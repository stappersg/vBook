## Delivery sub-system

The delivery subsystem uses specific actions. They can be called at any vSMTP stages.

### Delivering local mails

The incoming mail traffic can locally be delivered using :

- The [Mbox] format 
- The [Maildir] format

[Mbox]: https://datatracker.ietf.org/doc/html/rfc4155
[Maildir]: https://en.wikipedia.org/wiki/Maildir

&#9762; | The Local Mail Transfer Protocol ([LMTP]) is currently not implemented.

[LMTP]: https://en.wikipedia.org/wiki/Local_Mail_Transfer_Protocol

### Delivering distant mails

vSMTP uses a well known and secured third-party software [Lettre] also written in Rust.

[Lettre]: https://github.com/lettre/lettre

### Specific actions for the deliver stage

| Action | Syntax | Description |
| ---- | ---- | ---- |
| Deliver | deliver(ctx, proto) | Delivery using protocol.
| Forward | forward(ctx, addr) | Forward mail to an other MTA.

Protocol are "smtp", "mbox" and "maildir", "default" and "none".

The default behavior can be set in the TOML configuration file.
