# Features

vSMTP is a Mail Transfer Agent ([MTA]) and a Mail Submission Agent ([MSA]). It is not intended to be a Mail User Agent ([MUA]) nor a Mail Delivery Agent ([MDA]).

For outgoing mail, vSMTP can directly be addressed by your MUA using the SMTP protocol.

For incoming mails, vSMTP can store messages on a server file-system using [Mbox] or [Maildir] formats. To retrieve emails from a remote client (MUA) it is necessary to install a MDA that can handle [POP] and/or [IMAP] protocols.

[MUA]: /src/term/agent.md#mua-mail-user-agent
[MTA]: /src/term/agent.md#mta-mail-transfer-agent
[MSA]: /src/term/agent.md#msa-mail-submission-agent
[MDA]: /src/term/agent.md#mda-mail-delivery-agent

[mbox]: https://en.wikipedia.org/wiki/Mbox
[maildir]: https://en.wikipedia.org/wiki/Maildir

[POP]: https://en.wikipedia.org/wiki/Post_Office_Protocol
[IMAP]: https://en.wikipedia.org/wiki/Internet_Message_Access_Protocol

## Roadmap

Take a look at the [milestones](https://github.com/viridIT/vSMTP/milestones) for vSMTP to get an overview of what will be added in future releases.

Follow the development, plannings and announcements for incoming features on the [official discord server](https://discord.gg/N8JGBRBshf).

## Available features

### Networking

The core of vSMTP uses high performance asynchronous connections to supports heavy workloads.

- It can listen and serve on multiple addresses.
- Supports IPv4 and IPv6 formats.
- Handle one or multiple emails per connections.
- Is compliant with [Internet Message Format] and [Simple Mail Transfer Protocol] RFCs.
- [TLS 1.3] support.
- Exposes complete DNS configurations (thanks to Benjamin Fry's [Trust-DNS] crate).

[Internet Message Format]: https://datatracker.ietf.org/doc/html/rfc5322
[Simple Mail Transfer Protocol]: https://datatracker.ietf.org/doc/html/rfc5321
[TLS 1.3]: https://datatracker.ietf.org/doc/html/rfc8446
[Trust-DNS]: https://github.com/bluejekyll/trust-dns

### Filtering

vSMTP exposes a complete filtering system. In addition to the standard analysis of the SMTP envelope, vSMTP provides on the fly interactions with headers of the email. Users can generate complex routing and filtering scenarios through a simple and intuitive scripting language.

- [vSMTP scripting language] allowing administrators to define complex filtering rules.
- Before and after queueing filtering.
- Interaction at each SMTP state (CONNECT, HELO/EHLO, MAIL, RCPT, DATA).

Interacting with the body of the email (MIME) is planned for future releases.

[vSMTP Scripting Language]: /src/filtering/vsl.md

### Extensions

vSMTP is a modular and highly customizable product supporting plugins developed in the [Rust programing language].

Some plugins are already available.

- CSV file databases.
- MySQL databases.
- System commands execution.
- Third-party software integration via delegation using the SMTP protocol.

Other plugins like LDAP, NoSQL databases, in-memory caches, Compliancy with [Postfix SMTP access policy delegation] and Unix/IP socket calls are being planned for future releases.

[Postfix SMTP access policy delegation]: http://www.postfix.org/SMTPD_POLICY_README.html
[Rust programing language]: https://www.rust-lang.org/

### Delivery

vSMTP is able to deliver emails remotely or locally.

- SMTP remote delivery - using [Lettre].
- SMTP forwarding.
- Mbox and Maildir formats for local delivery.

[Lettre]: https://github.com/lettre/lettre

### Email authentication mechanisms

vSMTP secures the email traffic by implementing the following mechanisms.

- Message submission RFCs.
- [SPF] support.
- [DKIM] signer and verifier.
- [DMARC] verifier. (reporting is not natively supported)
- [Null MX] RFC.

[DANE], [ARC] and [BIMI] RFCs are planned for future releases.

[Null MX]: https://www.rfc-editor.org/rfc/rfc7505.html
[DANE]: https://www.rfc-editor.org/rfc/rfc7671.html
[SPF]: https://www.rfc-editor.org/rfc/rfc7208.html
[DKIM]: https://www.rfc-editor.org/rfc/rfc6376.html
[DMARC]: https://www.rfc-editor.org/rfc/rfc7489.html
[ARC]: https://www.rfc-editor.org/rfc/rfc8617.html
[BIMI]: https://datatracker.ietf.org/wg/bimi/about/
