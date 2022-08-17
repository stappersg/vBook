# Features

vSMTP is a Mail Transfer Agent ([MTA]) and a Mail Submission Agent ([MSA]).

It is not intended to be a Mail User Agent ([MUA]) nor a Mail Delivery Agent ([MDA]).

For outgoing mail, vSMTP can directly be addressed by your [MUA] using the SMTP protocol.

For incoming mails, vSMTP can deliver local mail to a client storage using mbox or maildir formats. To retrieve emails from your [MUA] it is necessary to install a [MDA] that can handle POP and/or IMAP protocols.

&#9758; | About MDA: For Debian/Ubuntu server the most straightforward solution is to download and install [courier-imap] package and to specify where the `MailDir` folders are located.

[courier-imap]: https://packages.debian.org/search?keywords=courier-imap

[MUA]: ./term/agent.html#mua-mail-user-agent
[MTA]: ./term/agent.html#mta-mail-transfer-agent
[MSA]: ./term/agent.html#msa-mail-submission-agent
[MDA]: ./term/agent.html#mda-mail-delivery-agent

## Roadmap

Take a look at the [ROADMAP](https://github.com/viridIT/vSMTP/blob/develop/ROADMAP.md) in vSMTP repository.

Follow the development of vsmtp, plannings and announcements for incoming features on the [official discord server](https://discord.gg/N8JGBRBshf).

## Available features

### Networking

- Listen and serve on multiple addresses.
- Support for IPv4 and IPv6 format.
- Built on high performance asynchronous connections.
- Handle one or multiple emails per connections.
- Compliancy with [Internet Message Format] and [Simple Mail Transfer Protocol] RFCs.
- [TLS 1.3] support.
- Complete DNS configurations (thanks to Benjamin Fry's [Trust-DNS] crate).
- Support for high workload through built-in mechanisms.

[Internet Message Format]: https://datatracker.ietf.org/doc/html/rfc5322
[Simple Mail Transfer Protocol]: https://datatracker.ietf.org/doc/html/rfc5321
[TLS 1.3]: https://datatracker.ietf.org/doc/html/rfc8446
[Trust-DNS]: https://github.com/bluejekyll/trust-dns

### API

vSMTP is a modular and highly customizable product.  Adding or modifying subsystems is made easier by the internal design of the software. An API is available and allows easy integration into existing security elements. Several native plug-ins are already available.

- Mail exports in RAW and JSON format.
- Third-party software called by user-defined services.
- Mods and addons support.
- Applications logs.

### Filtering

vSMTP has a complete filtering system. In addition to the standard analysis of the SMTP envelope, vSMTP provides on the fly interactions on the content of messages (MIME). Users can generate complex routing and filtering scenarios through a simple and intuitive advanced scripting language.

- Before and after queueing filtering.
- [vSMTP scripting language] allowing administrators to define complex rules.
- Interaction at each SMTP state (HELO/EHLO, CONNECT, MAIL, RCPT, DATA).

[vSMTP Scripting Language]: reference/vSL/vsl.md

### Delivery

- SMTP remote delivery - using a third-party software, [Lettre].
- [Mbox] and [Maildir] format for local delivering.
- SMTP relaying and forwarding.

[Mbox]: https://datatracker.ietf.org/doc/html/rfc4155
[Maildir]: https://en.wikipedia.org/wiki/Maildir
[Lettre]: https://github.com/lettre/lettre

### External services

vSMTP supports SMTP delegation, command calls, and file databases.
Next versions will provide SQL and NoSQL databases and in-memory caches supports. Compliancy with [Postfix SMTP access policy delegation] and Unix/IP socket calls are planned for Q3/2022.

[Postfix SMTP access policy delegation]: http://www.postfix.org/SMTPD_POLICY_README.html

### Email authentication mechanisms

- Message submission RFCs.
- [Null MX] RFC.
- [SPF] support.
- [DKIM] signer and verifier.  
- [DMARC] is planned for the next minor release.
- [DANE] protocol is planned for future release.
- [ARC] and [BIMI] experimental and future Internet standards are currently not supported.

[Null MX]: https://www.rfc-editor.org/rfc/rfc7505.html
[DANE]: https://www.rfc-editor.org/rfc/rfc7671.html
[SPF]: https://www.rfc-editor.org/rfc/rfc7208.html
[DKIM]: https://www.rfc-editor.org/rfc/rfc6376.html
[DMARC]: https://www.rfc-editor.org/rfc/rfc7489.html
[ARC]: https://www.rfc-editor.org/rfc/rfc8617.html
[BIMI]: https://tools.ietf.org/id/draft-blank-ietf-bimi-00.html
