## Delivery sub-system

The delivery subsystem uses specific actions. They can be called at any vSMTP stages.

### Delivering local mails

The incoming mail traffic can locally be delivered using :

- The [Mbox] format.
- The [Maildir] format.

[Mbox]: https://datatracker.ietf.org/doc/html/rfc4155
[Maildir]: https://en.wikipedia.org/wiki/Maildir

&#9762; | The Local Mail Transfer Protocol ([LMTP]) is currently not implemented.

[LMTP]: https://en.wikipedia.org/wiki/Local_Mail_Transfer_Protocol

### Delivering distant mails

vSMTP uses a well known and secured third-party software [Lettre] also written in Rust.

[Lettre]: https://github.com/lettre/lettre

### Specific actions for the deliver stage

| Action      | Syntax                 | Description                                                   |
| ----------- | ---------------------- | ------------------------------------------------------------- |
| Deliver     | deliver(rcpt)          | simple delivery for a single recipient.                       |
| Deliver All | deliver_all()          | simple delivery for all recipients.                           |
| Forward     | forward(rcpt, addr)    | Forward mail to an other MTA for a single recipient.          |
| Forward     | forward_all(addr)      | Forward mail to an other MTA for all recipients.              |
| Maildir     | maildir(rcpt)          | deliver the email locally via maildir for a single recipient. |
| Maildir     | maildir_all()          | deliver the email locally via maildir for all recipients.     |
| Mailbox     | mbox(rcpt)             | deliver the email locally via mbox for a single recipient.    |
| Mailbox     | mbox_all()             | deliver the email locally via mbox for all recipients.        |
| No delivery | disable_delivery(rcpt) | disable the delivery for a single recipient.                  |
| No delivery | disable_delivery_all() | disable the delivery for all recipients.                      |
