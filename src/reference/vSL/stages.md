# vSL stages and SMTP states

vSMTP can interact with the messaging transaction at multiple levels. These are related to the states defined in the SMTP protocol.

At each step vSL updates a global context containing transaction and mail data.

## vSMTP stages

Here is a list of available stages in order of evaluation.

| Stage   | SMTP state                 | Context available               |
| :------ | :------------------------- | :------------------------------ |
| connect | Before HELO/EHLO command   | Connection related information. |
| helo    | After HELO/EHLO command    | HELO string.                    |
| mail    | After MAIL FROM command    | Sender address.                 |
| rcpt    | After each RCPT TO command | The entire SMTP envelop.        |
| preq    | Before queuing[^preq]      | The entire mail.                |
| postq   | After queuing[^postq]      | The entire mail.                |
| deliver | Before delivering          | The entire mail.                |

[^preq]: Preq stage triggers after the end of receiving data from the client, just before the server answer back with a 250 code.
[^postq]: Postq stage triggers after the preq stage, when the connection closes and the SMTP code was sent to the client.

Stages are declared in a `main.vsl` file like this:

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

Stages do not need to be declared in order, but it is a good practice to do so.

## Before queueing vs. after queueing

vSMTP can process mails before the incoming SMTP mail transfer completes and thus rejects inappropriate mails by sending an SMTP error code and closing the connection.

This early detection of inappropriate mails has several advantages :

- The responsibility is on the remote SMTP client side,
- It consumes less CPU and disk resources,
- The system is more reactive.

However as the SMTP transfer must end within a deadline, a system facing a heavy workload may have difficulties to respond in time.

To protect against bursts and crashes, vSMTP implements several internal mechanisms like 'delay-variation' or 'temporary service unavailable messages', in accordance with the SMTP RFCs.

## Context variables

As described above, depending on the stage, vSL exposes data to the end user.
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

&#9762; | the "mail context" (data obtained through the `Connection` and `Transaction` modules) is unique for each incoming connexion.
