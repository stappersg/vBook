## Delivery sub-system

The delivery subsystem uses 

These methods can be called at any vSMTP stages. 

### Delivering local mails

For incoming mail, vSMTP can locally deliver it using :

- The [Mbox] format 
- The [Maildir] format

[Mbox]: https://datatracker.ietf.org/doc/html/rfc4155
[Maildir]: https://en.wikipedia.org/wiki/Maildir

&#9762; | [LMTP] (Local Mail Transfer Protocol) is currently not implemented.

[LMTP]: https://en.wikipedia.org/wiki/Local_Mail_Transfer_Protocol

### Delivering distant mails

vSMTP uses a well known and secured third-party software, also written in Rust : [Lettre]

[Lettre]: https://github.com/lettre/lettre

### Specific actions for the deliver stage

| Action | Syntax | Description |
| ---- | ---- | ---- |
| USE_SMTP | USE_SMTP() | Remote delivery using SMTP protocol.
| USE_MAILDIR | USE_MAILDIR() | Local delivery using Maildir format.
| USE_MBOX | USE_MBOX() | Local delivery using Mbox format.
| NO_DELIVERY | NO_DELIVERY() | Prevent the system from delivering the email.
| FORWARD | FORWARD(addr \| fqdn) | Forward mail to an other MTA.
