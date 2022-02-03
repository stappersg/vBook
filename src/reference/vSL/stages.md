## vSL stages and SMTP states

vSMTP can interact with the messaging transaction at multiple levels. These are related to the states defined in the SMTP protocol.

To do this, vSL publishes a global context which is updated with each step change.

### vSMTP stages

| Stage | SMTP state | Context available
| :--- | :--- | :---
| connect | Before HELO/EHLO command | Connection related information.
| helo | After HELO/EHLO command | HELO string.
| mail | After MAIL FROM command | Sender address.
| rcpt | After RCPT TO command | The entire SMTP envelop
| preq | Before queuing the mail | The entire mail.
| postq | After queuing the mail | The entire mail.

?????????????? DELIVER stage ???????????????

> Note about `preq` and `postq` stages:
> - Preq stage triggers after the end of data, before the server answer (ex. 250 OK). 
> - Postq stage triggers when Connection is already closed and the SMTP code sent.

### Before queueing vs. after queueing

vSMTP can process mails before the incoming SMTP mail transfer completes and thus rejects inappropriate mails by sending an SMTP error code and closing the connection.

This early detection of inappropriate mails has several advantages :

- the responsibility is on the remote SMTP client side,
- it consumes less CPU and disk resources,
- the system is more reactive.

However as the SMTP transfer must end within a deadline, a system facing a heavy workload may have difficulties to respond in time.

To protect against bursts and crashes, vSMTP implements several internal mechanisms like 'delay-variation' or 'temporary service unavailable messages', in accordance with the SMTP RFCs.

### Context variables

Message related variables are available depending on the stage.

| Stage | Name | Type | Description
| :--- | :--- | :--- | :--- 
| Connect | ${connect} | ip4/ip6 | Source IP address.
| | ${port} | int | Source port.
| | ${date} | string | Current date.
| | ${time} | string | Current time.
| helo | ${helo} | string | HELO/EHLO SMTP value |
| mail | ${mail.full}| addr | Sender email address. ${mail} is equivalent.
| | ${mail.local_part} | string | Sender name.
| | ${mail.domain} | fqdn | Sender fqdn.
| rcpt | ${rcpt.full} | addr | Current recipient address. ${rcpt} is equivalent.
| | ${rcpt.local_part} | string | Current sender name.
| | ${rcpt.domain} | fqdn | Current sender fqdn.
| | ${rcpts.full} | Array of addr| Recipients addresses. ${rcpts} is equivalent.
| | ${rcpts.local_parts} | Array of string | Senders name.
| | ${rcpts.domains} | Array of fqdn | Senders fqdn.
| preq |  ${data} |
| postq |
| deliver |

????????????? RAW DATA variable ??

>Please note that the `rcpts` array is completely filled at PREQ stage and not in RCPT stage.

??? preq ???? in this stage, every built-in variables are filled. You can do complex rule matching in this stage.

### Connection vs mail transaction

As defined in the SMTP RFCs, a single connection can handle several mail transactions.

HELO 

\> MAIL FROM > RCPT TO > DATA

\> MAIL FROM > RCPT TO > DATA 

\> [...]

\> QUIT
