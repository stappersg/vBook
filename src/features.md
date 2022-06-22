# Features

vSMTP is a secured, faster and greener Mail Transfer Agent.

It is a more efficient, more secure and more ergonomic product than the competition. It is up to 10 times faster than its competitors and significantly reduces the need for IT resources.

It is developed in Rust. Compared to solutions developed in C / C ++, Rust guarantees the absence of segmentation errors and race conditions. It is the latest generation language best suited to system programming, network services and embedded systems.

Its development goes through a full cycle of testing. Static and dynamic tests allow more comprehensive coverage of safety tests, one covering faults of the other and vice versa (static view and runtime view).

## Networking

The network code has been designed with performance and load resistance as the main objectives.

- Support for IPv4 and IPv6 format.
- Built on high performance asynchronous connections.
- Handling of multiple emails per transaction.
- Compliancy with [Internet Message Format] and [Simple Mail Transfer Protocol] RFCs.
- [TLS 1.3] support.
- Complex DNS configurations - thanks to Benjamin Fry's [Trust-DNS] crate.
- Support for high workload through built-in mechanisms.


[Internet Message Format]: https://datatracker.ietf.org/doc/html/rfc5322
[Simple Mail Transfer Protocol]: https://datatracker.ietf.org/doc/html/rfc5321
[TLS 1.3]: https://datatracker.ietf.org/doc/html/rfc8446
[Trust-DNS]: https://github.com/bluejekyll/trust-dns

## API

vSMTP is modular and highly customizable.  Adding or modifying subsystems is facilitated by the internal design of the software. An API is available allowing easy integration into existing security elements. Several native plug-ins are already available.

- Mail exports in raw and json format.
- Third-party softwares called by user-defined services.
- Mods and addons support.
- Applications logs.

## Filtering

vSMTP has a complete filtering system. In addition to the standard analysis of the SMTP envelope, the product adds the possibility of interacting on the fly on the content of messages (MIME). It is possible to filter, modify, encrypt, etc. any part of an email. Users can generate complex routing and filtering scenarios through a simple and intuitive advanced scripting language.

- Before and after queueing filtering.
- [vSMTP scripting language] allowing administrators to define complex rules.
- Interaction at each SMTP state (HELO/EHLO, CONNECT, MAIL, RCPT, DATA).

[vSMTP Scripting Language]: reference/vSL/vsl.md

## Delivery

vSMTP is a Mail Transfer Agent (MTA) and is not intended to be a Mail User Agent (MUA) or a Mail Delivery Agent (MDA). For outgoing mail, vSMTP can directly be addressed by your email client (MUA) using the SMTP protocol. For incoming mails, vSMTP can deliver local mail to a client storage using mbox or maildir formats.

- SMTP remote delivery - using a third-party software, [Lettre].
- [Mbox] and [Maildir] format for local delivering.
- SMTP relaying and forwarding.

[Mbox]: https://datatracker.ietf.org/doc/html/rfc4155
[Maildir]: https://en.wikipedia.org/wiki/Maildir
[Lettre]: https://github.com/lettre/lettre

## External services

vSMTP supports SMTP delegation, command calls and file databases.
Next versions will bring SQL and NoSQL databases and in-memory caches supports. Compliancy with [Postfix SMTP access policy delegation] and Unix/IP socket calls are planned for Q3/2022.

[Postfix SMTP access policy delegation]: http://www.postfix.org/SMTPD_POLICY_README.html

## Email authentication mechanisms

- Message submission RFCs.
- [SPF] support
- [DANE] protocol, [DKIM] and [DMARC] mechanisms supports are planned for future release.
- [ARC] and [BIMI] experimental and future Internet standards are currently not supported.

[DANE]: https://www.rfc-editor.org/rfc/rfc7671.html 
[SPF]: https://www.rfc-editor.org/rfc/rfc7208.html
[DKIM]: https://www.rfc-editor.org/rfc/rfc6376.html
[DMARC]: https://www.rfc-editor.org/rfc/rfc7489.html
[ARC]: https://www.rfc-editor.org/rfc/rfc8617.html
[BIMI]: https://tools.ietf.org/id/draft-blank-ietf-bimi-00.html
