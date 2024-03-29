The vSMTP reference guide
==========================

<!-- Use 🆕 when updating chapters, remove them after a given time -->

[The vSMTP Book](index.md)

----------------------

[Features](features.md)

# Getting Started

- [Installation](get-started/installation.md)
  - [Linux](get-started/installation/linux.md)
  - [BSD 🚧]()
  - [Cargo](get-started/installation/cargo.md)
  - [Docker](get-started/installation/docker.md)
- [Concepts](get-started/concepts.md)
- [Configuration File Structure](get-started/config-file-struct.md)
  - [Root configuration](get-started/config-file-struct/root.md)
  - [Filtering](get-started/config-file-struct/filtering.md)
  - [Objects](get-started/config-file-struct/objects.md)
  - [Plugins](get-started/config-file-struct/plugins.md)
  - [Services](get-started/config-file-struct/services.md)
- [Running vSMTP](get-started/running.md)

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
  - [ARC 🚧]()
  - [BIMI 🚧]()
  - [DANE 🚧]()

- [Plugins](plugins/plugins.md)
  - [Command](plugins/command.md)
  - [SMTP](plugins/smtp.md)
  - [CSV](plugins/csv.md)
  - [MySQL](plugins/mysql.md)

# Reference

- [Configuration Parameters](ref/config/config.md)
- [vSL's API](ref/vSL/api.md)
  - [Standard Functions](ref/vSL/functions.md)
    - [Rule State](ref/vSL/api/fn::global::state.md)
    - [Logging](ref/vSL/api/fn::global::logging.md)
    - [Mail Context](ref/vSL/api/fn::global::ctx.md)
    - [Envelop](ref/vSL/api/fn::global::envelop.md)
    - [Message](ref/vSL/api/fn::global::msg.md)
    - [Authentication](ref/vSL/api/fn::global::auth.md)
    - [SPF](ref/vSL/api/fn::global::spf.md)
    - [DKIM](ref/vSL/api/fn::global::dkim.md)
    - [DMARC](ref/vSL/api/fn::global::dmarc.md)
    - [DNS](ref/vSL/api/fn::global::dns.md)
    - [Transports](ref/vSL/api/fn::global::transport.md)
    - [File System](ref/vSL/api/fn::global::fs.md)
    - [Time](ref/vSL/api/fn::global::time.md)
    - [Utils](ref/vSL/api/fn::global::utils.md)
    - [Codes](ref/vSL/api/fn::global::code.md)
    - [Network](ref/vSL/api/fn::global::net.md)
    - [Objects](ref/vSL/api/fn::global::obj.md)
  - [Variables](ref/vSL/variables.md)
    - [Configuration](ref/vSL/api/var::cfg.md)
  - [Plugins](ref/vSL/plugins.md)
    - [Cmd](ref/vSL/api/fn::global::cmd.md)
    - [Smtp](ref/vSL/api/fn::global::smtp.md)
    - [MySQL](ref/vSL/api/fn::global::mysql.md)
    - [Memcached](ref/vSL/api/fn::global::memcached.md)
    - [Ldap](ref/vSL/api/fn::global::ldap.md)

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
- [What is DMARC ? 🚧]()
- [Dealing with Null MX records](term/nullmx.md)

# Development

- [Building from source](dev/build/source.md)
  - [Linux](dev/build/source/linux.md)
  - [FreeBSD](dev/build/source/freebsd.md)
- [The Queue System](dev/queues.md)
- [Create plugins](dev/plugins/plugins.md)

# Appendix

- [Acknowledgements](appendix/acknowledgements.md)
