# Stages

vSMTP interacts with the messaging transaction at all states defined in the SMTP protocol.
At each step, vSL updates a global context containing transaction and mail data accessible in rules.

## vSMTP stages

Available stages in order of evaluation:

| Stage        | SMTP state                 | Context available               |
| :----------- | :------------------------- | :------------------------------ |
| connect      | Before HELO/EHLO command   | Connection related information. |
| authenticate | After AUTH command         | Connection related information. |
| helo         | After HELO/EHLO command    | HELO string.                    |
| mail         | After MAIL FROM command    | Sender address.                 |
| rcpt         | After each RCPT TO command | List of recipients.             |
| preq         | Before queuing[^preq]      | The entire mail.                |
| postq        | After queuing[^postq]      | The entire mail.                |
| delivery     | Before delivering          | The entire mail.                |

[^preq]: Preq stage triggers after the end of receiving data from the client, just before the server answers back with a 250 code.

[^postq]: Postq stage triggers after the preq stage, when the connection closes and the SMTP code is sent to the client.

## Syntax

Stages are declared in `.vsl` files using the following syntax:

```js
#{
    connect: [
        // rules, actions, delegations ...
    ],

    mail: [
        // rules, actions, delegations ...
    ],

    postq: [
        // rules, actions, delegations ...
    ],

    // other stages ...
}
```

> Stages do not need to be declared in the previous given order, but it is a good practice.


## Rules

Rules are combined with stages in `.vsl` files.


```js
#{
    connect: [
        // This rule is executed once a new client connects to the server.
        rule "check client ip" || {
            if client_ip() == "192.168.1.254" {
                faccept()
            } else {
                next()
            }
        }
    ],

    mail: [
        // This action is executed once the server receive the "MAIL FROM" command.
        action "log incoming transaction" || {
            // Logging to /var/log/vsmtp.
            log("info", `new transaction from ${mail_from()} at ${client_ip()}`);
        }
    ],
}
```

Using stages, rules can be run at specific stages of the configuration, enabling precise email filtering.

## Before queueing vs. after queueing

vSMTP can process mails before the incoming SMTP mail transfer completes and thus rejects inappropriate mails by sending an SMTP error code and closing the connection.

The advantages of an early detection of unwanted mails are:

- The responsibility is on the remote SMTP client side.
- It consumes less CPU and disk resources.
- The system is more reactive.

However, as the SMTP transfer must to be completed within a deadline, heavy workload may cause a system to fail to respond in time.

To protect against bursts and crashes, vSMTP implements several internal mechanisms like 'delay-variation' or 'temporary service unavailable messages', in conformance with the SMTP RFCs.

## Context variables

As described above, depending on the stage, vSL exposes data that can be accessed with functions.
Check out both [Connection](api/Connection.md) and [Transaction](api/Transaction.md) modules.

## Connection vs mail transaction

As defined in the SMTP RFCs, a single connection can handle several mail transactions.

```shell
[... connection from an IP]
HELO                                    # Start of SMTP transaction
    > MAIL FROM > RCPT TO > DATA        # First mail
    > MAIL FROM > RCPT TO > DATA        # Second mail
    > [...]
QUIT                                    # End of transaction
```

&#9762; | The "mail context" (data obtained from the `Connection` and `Transaction` modules) is unique for each incoming connection.


TODO: add the following section to this chapter.

## Rules and vSMTP Stages

Rules are bound to a vSMTP stage. Stages that are not used can be omitted, but must appear only once if used. They are declared in the `main.vsl` file.

```js
// -- objects.vsl

export const my_company = fqdn("mycompany.net");

//-- main.vsl

import "objects" as obj;

#{
    connect: [
        action "log connect" || log("warn", `Connection from : ${client_ip()}`),
        rule "check connect" || if client_ip() == "192.168.1.254" { next() } else { deny() },
    ],

    rcpt: [
        rule "local_domain" || {
            if obj::my_company == rcpt().domain { next() } else { deny() }
        },
    ],

    preq: [
        action "rewrite recipients" || {
            rewrite_rcpt_envelop("johndoe@compagny.com", "john.doe@company.net");
            remove_rcpt("customer@company.net");
            add_rcpt("no-reply@company.net");
        },
    ],

    // ... other rules & actions
}
```

## Implicit rules

For security purpose, end-users should always add a trailing rule at the end of a stage. However, to avoid undefined behavior, an implicit trailing rule is set to `next()`, moving the rule engine to the next stage.

```js
//-- objects.vsl

export const my_company = fqdn("mycompany.net");

//-- main.vsl
import "objects" as obj;

#{
    rcpt: [
        rule "local domain" || {
            if obj::my_company == rcpt().domain { accept() } else { next() }
        },

        // ... other rules / actions

        // Trailing rule (denying is the default behavior for rcpt stage)
        rule "default" || deny(),
    ]
}
```

> As with firewall rules, the best practice is to deny "everything" and only accept authorized and known clients (like the example above).
