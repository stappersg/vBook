# vSL stages and SMTP states

vSMTP can interact with the messaging transaction at multiple levels. These are related to the states defined in the SMTP protocol.

At each step vSL updates and publishes a global context containing transaction and mail data.

## vSMTP stages

| Stage | SMTP state | Context available
| :--- | :--- | :---
| connect | Before HELO/EHLO command | Connection related information.
| helo | After HELO/EHLO command | HELO string.
| mail | After MAIL FROM command | Sender address.
| rcpt | After RCPT TO command | The entire SMTP envelop.
| preq | Before queuing[^preq]  | The entire mail.
| postq | After queuing[^postq]  | The entire mail.
| deliver | Before delivering | The entire mail.

[^preq]: Preq stage triggers after the end of data, before the server answer (ex. 250 OK).

[^postq]: Postq stage triggers when Connection is already closed and the SMTP code sent.

## Before queueing vs. after queueing

vSMTP can process mails before the incoming SMTP mail transfer completes and thus rejects inappropriate mails by sending an SMTP error code and closing the connection.

This early detection of inappropriate mails has several advantages :

- the responsibility is on the remote SMTP client side,
- it consumes less CPU and disk resources,
- the system is more reactive.

However as the SMTP transfer must end within a deadline, a system facing a heavy workload may have difficulties to respond in time.

To protect against bursts and crashes, vSMTP implements several internal mechanisms like 'delay-variation' or 'temporary service unavailable messages', in accordance with the SMTP RFCs.

## Context variables

As described above, depending on the stage vSL exposes variables to the end user.

| Stage | Name | Type | Description
| :--- | :--- | :--- | :---
| Connect | client_addr | ip4/ip6 | Source IP address.
| | ${port} | int | Source port ?????????????
| | timestamp | POSIX timestamp | Connection timestamp
| Helo | helo | string | HELO/EHLO SMTP value.
| Mail | mail_from | addr | Sender email address.
| | mail_from.local_part | string | Sender name.
| | mail_from.domain | fqdn | Sender fqdn.
| Rcpt | rcpt | hash(addr) | Hash table containing all recipient addresses.
| | rcpt.local_part | hash(string) | Recipient names.
| | rcpt.domain | hash(fqdn) | Recipient fqdn.
| Next stages |  data | string | Email raw data.
|  | parse[^parse] | vec(struct) | Parsed email.

[^parse]: The `parse` variable is available only if the user triggers a `vSL.PARSE()` action.

These variables are part of the email context `ctx`. Thus must be called in a vSL file using the dot notation i.e. `ctx.timestamp`.

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

&#9762; | Per network connection, the "connect context" is unique while other variables like ${mail} are reset after each new message transaction.
