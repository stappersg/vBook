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
  - [Services](get-started/config-file-struct/services.md)

# Configuring vSMTP

- [Filtering](filtering/filtering.md)
  - [vSL - the vSMTP Scripting Language](filtering/vsl.md)
  - [Rules and Actions](filtering/rules.md)
  - [SMTP states and vSMTP stages](filtering/stages.md)
  - [Transaction context](filtering/transaction.md)
  - [Objects](filtering/objects.md)
  - [Delegation](filtering/delegation.md)
  - [Time](filtering/time.md)

- [Settings](settings/settings.md)
  - [Logging system](settings/logging.md)
  - [DNS configuration](settings/dns.md)
  - [DKIM](settings/dkim.md)
  - [ARC 🚧]()
  - [BIMI 🚧]()
  - [DANE 🚧]()

- [Plugins](plugins/plugins.md)
  - [Command](plugins/command.md)
  - [SMTP](plugins/smtp.md)
  - [CSV](plugins/csv.md)
  - [MySQL](plugins/mysql.md)

# Reference

- [vSL's API](ref/vSL/api.md)
  - [Standard Functions](ref/vSL/functions.md)
    - [Rule State](ref/vSL/api/fn::global::rule_state.md)
    - [Mail Context](ref/vSL/api/fn::global::mail_context.md)
    - [Message](ref/vSL/api/fn::global::message.md)
    - [Message Parsed](ref/vSL/api/fn::global::message_parsed.md)
    - [SPF](ref/vSL/api/fn::global::spf.md)
    - [DKIM](ref/vSL/api/fn::global::dkim.md)
    - [DMARC](ref/vSL/api/fn::global::dmarc.md)
    - [Transports](ref/vSL/api/fn::global::transports.md)
    - [Logging](ref/vSL/api/fn::global::logging.md)
    - [Write](ref/vSL/api/fn::global::write.md)
    - [Utils](ref/vSL/api/fn::global::utils.md)
    - [Types](ref/vSL/api/fn::global::types.md)
    - [Objects](ref/vSL/api/fn::global::objects.md)
    - [Rhai API (will be deprecated soon)](ref/vSL/api/fn::global::vsl-api.md)
  - [Variables](ref/vSL/variables.md)
    - [Configuration](ref/vSL/api/var::cfg.md)
    - [vSL API](ref/vSL/api/var::vsl-api.md)
  - [Plugins](ref/vSL/plugins.md)
    - [Cmd](ref/vSL/api/fn::global::cmd.md)
    - [Smtp](ref/vSL/api/fn::global::smtp.md)

# CLI

- [vsmtp](cli/vsmtp.md)
- [vqueue](cli/vqueue.md)

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
  - [DKIM](tuto/0/dkim.md)
  - [Antivirus](tuto/0/antivirus.md)
- [Greylist](tuto/1/greylist.md)
- [Using SPF](tuto/4/spf.md)
- [Using DKIM](tuto/3/dkim.md)
- [Using DMARC](tuto/5/dmarc.md)

# Trouble shooting

- [No logs available](troubles/nolog.md)

# Terminology

- [Mail Agent](term/agent.md)
- [Authentication Mechanisms](term/authentication.md)
- [What is SPF ?](term/spf.md)
- [What is DKIM ?](term/dkim.md)
- [Dealing with Null MX records](term/nullmx.md)

# Development

- [Building from source](dev/build/source.md)
  - [Linux](dev/build/source/linux.md)
  - [FreeBSD](dev/build/source/freebsd.md)
- [The Queue System](dev/queues.md)
- [Create plugins](dev/plugins/plugins.md)

# Appendix

- [Acknowledgements](appendix/acknowledgements.md)
