The vSMTP reference guide
==========================

[The vSMTP Book](index.md)

----------------------

[Features](features.md)

# Getting Started

- [Installation](get-started/installation.md)
- [Concepts](get-started/concepts.md)

# Tutorials

- [Doe's family](tuto/0/doe.md)
  - [Context](tuto/0/context.md)
  - [Basic configuration](tuto/0/basic.md)
  - [SSL/TLS](tuto/0/ssl-tls.md)
  - [Authentication](tuto/0/auth-sasl.md)
  - [Hardening vSMTP](tuto/0/hardening.md)
  - [Antivirus](tuto/0/antivirus.md)

# Advanced Settings

- [Logging system](advanced/logging.md)
- [DNS configuration](advanced/dns.md)
- [Virtual domains](advanced/virtual-domain.md)
- [Email authentication mechanisms](advanced/eam.md)
  - [Null MX](advanced/eam/nullmx.md)
  - [SPF](advanced/eam/spf.md)
  - [DKIM](advanced/eam/dkim.md)
  - [DMARC](advanced/eam/dmarc.md)
  - [ARC](advanced/eam/arc.md)
  - [BIMI](advanced/eam/bimi.md)
- [SMTP security using DANE](advanced/dane.md)

# Reference

- [Command line parameters](reference/command.md)
- [Complete vSMTP TOML key/value list](reference/config-file.md)
- [vSL - the vSMTP Scripting Language](reference/vSL/vsl.md)
  - [SMTP states and vSMTP stages](reference/vSL/stages.md)
  - [Rules](reference/vSL/rules.md)
  - [Objects](reference/vSL/objects.md)
  - [Delivery](reference/vSL/delivery.md)
  - [Services](reference/vSL/services.md)
  - [Time](reference/vSL/time.md)
  - [Advanced Usage](reference/vSL/advanced.md)
  - [vSL's API](reference/vSL/api.md)
    - [Status](reference/vSL/api/Status.md)
    - [Message](reference/vSL/api/Message.md)
    - [Envelop](reference/vSL/api/Envelop.md)
    - [Connection](reference/vSL/api/Connection.md)
    - [Transaction](reference/vSL/api/Transaction.md)
    - [Auth](reference/vSL/api/Auth.md)
    - [Security](reference/vSL/api/Security.md)
    - [Delivery](reference/vSL/api/Delivery.md)
    - [Services](reference/vSL/api/Services.md)
    - [Utils](reference/vSL/api/Utils.md)
    - [Variables](reference/vSL/api/Variables.md)

# Development

- [Building from source](dev/build/source.md)
  - [Linux](dev/build/source/linux.md)
  - [FreeBSD](dev/build/source/freebsd.md)
- [The Queue System](dev/queues.md)

# Trouble shooting

- [Logging](troubles/nolog.md)

# Terminology

- [Mail Agent](term/agent.md)
