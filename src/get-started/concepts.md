# Configuring vSMTP

## Configuration file

The vSMTP service (network, default directories, tls, etc.) can be configured by editing the `vsmtp.toml` file. Its default location is `/etc/vsmtp/vsmtp.toml`.

When starting vSMTP, the configuration file is read and entirely parsed. An error occurs when a key or a value is incorrect. The server **never crashes** if the configuration is successfully loaded.

Please refer to the [dedicated chapter guide on the configuration](../reference/config-file.html) for further details.

&#9758; | The vSMTP service must be restarted to apply changes.

## Configuring SMTP filtering rules

SMTP filtering is performed by the rule engine. You can modify the behavior of vSMTP using the simple but powerful programming language vSMTP Scripting Language (vSL).

Its syntax is similar to a configuration format, but with programmatic capabilities. It is based on four main concepts : `rules`, `actions`, `objects` and `services`.

Please refer to the [dedicated chapter guide on the `vSL`](../reference/vSL/vsl.md) for further details.

&#9758; | The vSMTP service must be restarted to apply changes.

## The `vsmtp.service` file

This file contains all the mandatory information to start the vSMTP service on Linux server using [systemd] as the system and service manager.

[systemd]: https://freedesktop.org/wiki/Software/systemd/

&#9762; | Do not modify this file unless being highly aware of the impacts of your changes.
