## vSL stages and SMTP states

vSMTP can interact with the messaging transaction at multiple levels. These are related to the states defined in the SMTP protocol.

At each step vSL updates and publishes a global context containing transaction and mail data.

### vSMTP stages

| Stage | SMTP state | Context available
| :--- | :--- | :---
| connect | Before HELO/EHLO command | Connection related information.
| helo | After HELO/EHLO command | HELO string.
| mail | After MAIL FROM command | Sender address.
| rcpt | After RCPT TO command | The entire SMTP envelop.
| preq | Before queuing  | The entire mail.
| postq | After queuing  | The entire mail.
| deliver | Before delivering | The entire mail.

&#9998; | About `preq` and `postq` stages:
- Preq stage triggers after the end of data, before the server answer (ex. 250 OK). 
- Postq stage triggers when Connection is already closed and the SMTP code sent.

### Before queueing vs. after queueing

vSMTP can process mails before the incoming SMTP mail transfer completes and thus rejects inappropriate mails by sending an SMTP error code and closing the connection.

This early detection of inappropriate mails has several advantages :

- the responsibility is on the remote SMTP client side,
- it consumes less CPU and disk resources,
- the system is more reactive.

However as the SMTP transfer must end within a deadline, a system facing a heavy workload may have difficulties to respond in time.

To protect against bursts and crashes, vSMTP implements several internal mechanisms like 'delay-variation' or 'temporary service unavailable messages', in accordance with the SMTP RFCs.

### Context variables

As described above, depending on the stage vSL exposes variables to the end user.

| Stage | Name | Type | Description
| :--- | :--- | :--- | :--- 
| Connect | ${connect} | ip4/ip6 | Source IP address.
| | ${port} | int | Source port.
| | ${date} | string | Current date.
| | ${time} | string | Current time.
| helo | ${helo} | string | HELO/EHLO SMTP value.
| mail | ${mail.full} or \${mail} | addr | Sender email address.
| | ${mail.local_part} | string | Sender name.
| | ${mail.domain} | fqdn | Sender fqdn.
| rcpt | ${rcpt.full} or \${rcpt} | addr | Current recipient address.
| | ${rcpt.local_part} | string | Current sender name.
| | ${rcpt.domain} | fqdn | Current sender fqdn.
| | ${rcpts.full} or \${rcpt} | addr[]| Recipients addresses.
| | ${rcpts.local_parts} | string[] | Senders names.
| | ${rcpts.domains} | fqdn[] | Senders fqdn.
| next stages |  ${data} | string | Email raw data.
|  | ${parse} | vec(struct) | Parsed email.

&#9998; | The `rcpts` array is completely filled at PREQ stage and not in RCPT stage.

&#9998; | The `${parse}` variable is available only if the user triggers a `vSL.PARSE()` action.

### Connection vs mail transaction

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
