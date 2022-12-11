The vSMTP reference guide
==========================

[The vSMTP Book](index.md)

----------------------

[Features](features.md)

# Getting Started

- [Installation](get-started/installation.md)
- [Concepts](get-started/concepts.md)
- [Configuration File Structure](get-started/config-file-struct.md)
  - [Root configuration](get-started/config-file-struct/root.md)
  - [Filtering](get-started/config-file-struct/filtering.md)
  - [Objects](get-started/config-file-struct/objects.md)
  - [Plugins](get-started/config-file-struct/plugins.md)

# Configuring vSMTP

- [Filtering](filtering/filtering.md)
  - [vSL - the vSMTP Scripting Language](filtering/vsl.md)
  - [Rules](filtering/rules.md)
  - [SMTP states and vSMTP stages](filtering/stages.md)
  - [Transaction context](filtering/transaction.md)
  - [Objects](filtering/objects.md)
  - [Delegation](filtering/delegation.md)
  - [Time](filtering/time.md)

- [Settings](settings/settings.md)
  - [Logging system](settings/logging.md)
  - [DNS configuration](settings/dns.md)
  - [DMARC](settings/dmarc.md)
  - [ARC 🚧]()
  - [BIMI 🚧]()
  - [DANE 🚧]()

# Reference

- [Command line parameters](ref/command.md)
- [vSMTP Configuration reference](ref/config-file.md)
- [vSL's API](ref/vSL/api.md)
  - [Functions](ref/vSL/functions.md)
    - [SPF](ref/vSL/api/fn::global::spf.md)
    - [DKIM](ref/vSL/api/fn::global::dkim.md)
    - [DMARC](ref/vSL/api/fn::global::dmarc.md)
    - [Logging](ref/vSL/api/fn::global::logging.md)
    - [Mail Context](ref/vSL/api/fn::global::mail_context.md)
    - [Message](ref/vSL/api/fn::global::message.md)
    - [Message Parsed](ref/vSL/api/fn::global::message_parsed.md)
    - [Rule State](ref/vSL/api/fn::global::rule_state.md)
    - [Transports](ref/vSL/api/fn::global::transports.md)
    - [Types](ref/vSL/api/fn::global::types.md)
    - [Utils](ref/vSL/api/fn::global::utils.md)
    - [vSL Objects](ref/vSL/api/fn::global::vsl-objects.md)
    - [vSL Cmd](ref/vSL/api/fn::global::vsl-cmd.md)
    - [vSL SMTP](ref/vSL/api/fn::global::vsl-smtp.md)
    - [vSL API](ref/vSL/api/fn::global::vsl-api.md)
    - [Write](ref/vSL/api/fn::global::write.md)
  - [Variables](ref/vSL/variables.md)
    - [Configuration](ref/vSL/api/var::cfg.md)
    - [vSL API](ref/vSL/api/var::vsl-api.md)

- [Plugins](ref/plugins.md)
  - [Command](ref/plugins/command.md)
  - [SMTP](ref/plugins/smtp.md)
  - [CSV](ref/plugins/csv.md)
  - [MySQL](ref/plugins/mysql.md)

# Tutorials

- [Doe's family](tuto/0/doe.md)
  - [Context](tuto/0/context.md)
  - [Basic configuration](tuto/0/basic.md)
  - [Filtering](tuto/0/filtering.md)
    - [Incoming messages](tuto/0/filtering/incoming.md)
    - [Outgoing messages](tuto/0/filtering/outgoing.md)
    - [Internal messages](tuto/0/filtering/internal.md)
  - [SSL/TLS](tuto/0/ssl-tls.md)
  - [SPF](tuto/0/spf.md)
    - [Filtering](tuto/0/spf/filtering.md)
    - [What is SPF ?](tuto/0/spf/details.md)
  - [DKIM](tuto/0/dkim.md)
    - [Filtering](tuto/0/dkim/filtering.md)
    - [What is DKIM ?](tuto/0/dkim/details.md)
  - [Antivirus](tuto/0/antivirus.md)
- [Greylist](tuto/1/greylist.md)
- [Dealing with Null MX records](tuto/2/nullmx.md)

# Terminology

- [Mail Agent](term/agent.md)
- [Authentication Mechanisms](term/authentication.md)

# Trouble shooting

- [Logging](troubles/nolog.md)

# Development

- [Building from source](dev/build/source.md)
  - [Linux](dev/build/source/linux.md)
  - [FreeBSD](dev/build/source/freebsd.md)
- [The Queue System](dev/queues.md)

# Appendix

- [Acknowledgements](appendix/acknowledgements.md)
