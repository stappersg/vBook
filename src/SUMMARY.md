The vSMTP reference guide
==========================

[The vSMTP Book](index.md)

----------------------

[Features](features.md)

- [Getting Started](start/started.md)
  - [Requirements](start/requirements.md)
  - [Installation from packages](start/install/packages.md)
  - [Building from source](start/install/source.md)
    - [Linux](start/install/source/linux.md)
    - [FreeBSD](start/install/source/freebsd.md)
    - [OpenBSD]()
    - [NetBSD]()
  - [Step-by-step Configuration](start/configuration/configuration.md)
    - [Basic configuration](start/configuration/basic.md)
    - [Hardening vSMTP](start/configuration/hardening.md)
    - [Policy delegation](start/configuration/delegation.md)

- [Advanced settings](advanced/advanced.md)
  - [Server global and virtual domains parameters](advanced/toml.md)
  - [DNS configuration](advanced/dns.md)
  - [Email authentication mechanisms](advanced/eam.md)
    - [Null MX](advanced/eam/nullmx.md)
    - [SPF](advanced/eam/spf.md)
    - [DKIM](advanced/eam/dkim.md)
    - [DMARC](advanced/eam/dmarc.md)
    - [ARC](advanced/eam/arc.md)
    - [BIMI](advanced/eam/bimi.md)
  - [SMTP security using DANE](advanced/dane.md)
  - [Logging system](advanced/logging.md)
  - [Trouble shooting](advanced/troubleshooting.md)

- [Reference Guide]()
  - [Command line parameters](reference/command.md)
  - [Complete vSMTP TOML key/value list](reference/config-file.md)
  - [vSL - the vSMTP Scripting Language](reference/vSL/vsl.md)
    - [SMTP states and vSMTP stages](reference/vSL/stages.md)
    - [Objects](reference/vSL/objects.md)
    <!-- - [Functions](reference/vSL/functions.md) -->
    - [Rules](reference/vSL/rules.md)
    - [Delivery](reference/vSL/delivery.md)
    - [Services](reference/vSL/services.md)
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
- [Contribute]()
  - [The Queue System](development/queues.md)

Terminology
==========================

- [Mail Agent](term/agent.md)
