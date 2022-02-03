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
| preq | Before queuing the mail (2) | The entire mail.
| postq | After queuing the mail (3) | The entire mail.

?????????????? DELIVER stage ???????????????

> (1) After end of data, before server answer (ex. 250 OK).

> (2) Connection is already closed and the SMTP code sent.

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

RAW DATA variable ??

>Please note that the `rcpts` array is completely filled at PREQ stage and not in RCPT stage.

??? preq ???? in this stage, every built-in variables are filled. You can do complex rule matching in this stage.

### Connection vs mail transaction

As defined in the SMTP RFCs, a single connection can handle several mail transactions.

HELO 

\> MAIL FROM > RCPT TO > DATA

\> MAIL FROM > RCPT TO > DATA 

\> [...]

\> QUIT
