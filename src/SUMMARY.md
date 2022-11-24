The vSMTP reference guide
==========================

[The vSMTP Book](index.md)

----------------------

[Features](features.md)

# Getting Started

- [Installation](get-started/installation.md)
- [Concepts](get-started/concepts.md)
- [Configuration File Structure](get-started/config-file-struct.md)

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
    - [What is SPF ?](tuto/0/dkim/details.md)
  - [Antivirus](tuto/0/antivirus.md)
- [Greylist](tuto/1/greylist.md)

# Advanced Settings

- [Logging system](advanced/logging.md)
- [DNS configuration](advanced/dns.md)
- [Null MX](advanced/nullmx.md)
- [DMARC](advanced/dmarc.md)
- [ARC 🚧]()
- [BIMI 🚧]()
- [DANE 🚧]()

# Reference

- [Command line parameters](reference/command.md)
- [vSMTP Configuration reference](reference/config-file.md)
- [vSL - the vSMTP Scripting Language](reference/vSL/vsl.md)
  - [Rules](reference/vSL/rules.md)
  - [SMTP states and vSMTP stages](reference/vSL/stages.md)
  - [Transaction context](reference/vSL/transaction.md)
  - [Objects](reference/vSL/objects.md)
  - [Services](reference/vSL/services.md)
  - [Delegation](reference/vSL/delegation.md)
  - [Time](reference/vSL/time.md)
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
- [Plugins](reference/plugins.md)
  - [Command](reference/plugins/command.md)
  - [SMTP](reference/plugins/smtp.md)
  - [CSV](reference/plugins/csv.md)
  - [MySQL](reference/plugins/mysql.md)

# Development

- [Building from source](dev/build/source.md)
  - [Linux](dev/build/source/linux.md)
  - [FreeBSD](dev/build/source/freebsd.md)
- [The Queue System](dev/queues.md)

# Trouble shooting

- [Logging](troubles/nolog.md)

# Terminology

- [Mail Agent](term/agent.md)
- [Authentication Mechanisms](term/authentication.md)

# Appendix

- [Acknowledgements](appendix/acknowledgements.md)
