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
    - [What is DKIM ?](tuto/0/dkim/details.md)
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

- [Command line parameters](ref/command.md)
- [vSMTP Configuration reference](ref/config-file.md)
- [vSL - the vSMTP Scripting Language](ref/vSL/vsl.md)
  - [Rules](ref/vSL/rules.md)
  - [SMTP states and vSMTP stages](ref/vSL/stages.md)
  - [Transaction context](ref/vSL/transaction.md)
  - [Objects](ref/vSL/objects.md)
  - [Delegation](ref/vSL/delegation.md)
  - [Time](ref/vSL/time.md)
  - [vSL's API](ref/vSL/api.md)
    - [Status](ref/vSL/api/Status.md)
    - [Message](ref/vSL/api/Message.md)
    - [Envelop](ref/vSL/api/Envelop.md)
    - [Connection](ref/vSL/api/Connection.md)
    - [Transaction](ref/vSL/api/Transaction.md)
    - [Auth](ref/vSL/api/Auth.md)
    - [Security](ref/vSL/api/Security.md)
    - [Delivery](ref/vSL/api/Delivery.md)
    - [Services](ref/vSL/api/Services.md)
    - [Utils](ref/vSL/api/Utils.md)
    - [Variables](ref/vSL/api/Variables.md)
- [Plugins](ref/plugins.md)
  - [Command](ref/plugins/command.md)
  - [SMTP](ref/plugins/smtp.md)
  - [CSV](ref/plugins/csv.md)
  - [MySQL](ref/plugins/mysql.md)

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
