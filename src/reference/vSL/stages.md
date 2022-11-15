# Stages

vSMTP interacts with the messaging transaction at all states defined in the SMTP protocol.
At each step, vSL updates a context containing transaction and mail data accessible in rules.

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

Using stages, rules can be run at specific SMTP state, enabling precise email filtering.

> Stages that are not used are omitted, but must appear only once if used.
> ```js
> #{
>   connect: [],
>   // configuration error!
>   connect: [],
> }
> ```

## Recommandations

For security purpose, end-users should always add a trailing rule at the end of a stage.

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

        // If the client ip is not known, the connection is denied.
        rule "trailing" || deny(),
    ],
}
```

> As with firewall rules, the best practice is to deny "everything" and only accept authorized and known clients (like the example above).

## Before queueing vs. after queueing

> TL;DR
> `connect`, `authenticate`, `helo`, `mail`, `rcpt` and `preq` stages rules are run before an email is enqueued.
> `postq` and `delivery` stages rules are run after an email is enqueued and the server as received the complete email.

vSMTP can process mails before the incoming SMTP mail transfer completes and thus rejects inappropriate mails by sending an SMTP error code and closing the connection. This is possible by creating rules under the `connect`, `authenticate`, `helo`, `mail`, `rcpt` and `preq` stages.

The advantages of an early detection of unwanted mails are:

- The responsibility is on the remote SMTP client side.
- It consumes less CPU and disk resources.
- The system is more reactive.

However, as the SMTP transfer must to be completed within a deadline, heavy workload may cause a system to fail to respond in time.

Therefore, it is possible to handle an email "offline" when specifying rules under the `postq` and `delivery` stages.
The rules under those stages are run after the client received a 250 Ok code, after the server received the complete email. 

At this point, the rule engine is not able to send codes to the client even if the client sends multiple emails (each email is treated as a single entity by the rule engine), thus the rest of the rule engine behavior is considered "offline".

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