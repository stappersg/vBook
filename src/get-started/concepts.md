# Configuring vSMTP

## Configuration file

The vSMTP service (network, default directories, tls, etc.) can be configured by editing the `vsmtp.toml` file. Its default location is `/etc/vsmtp/vsmtp.toml`.

When starting vSMTP, the configuration file is read and entirely parsed. An error occurs when a key or a value is incorrect. The server **never crashes** if the configuration is successfully loaded.

Please refer to the [dedicated chapter guide on the configuration](../reference/config-file.html) for further details.

&#9758; | The vSMTP service must be restarted to apply changes.

## Configuring SMTP filtering rules

SMTP filtering is performed by the rule engine. The end user can interact and modify the behavior of vSMTP by adding objects and rules in `.vsl` configuration files. The `main.vsl` file in the `/etc/vsmtp/rules` folder is the entry point for the rules engine.

If there is no `.vsl` file declared, the server denies all incoming and outgoing mails, as well as domain forwarding. The `.vsl` files are commonly stored in the `/etc/vsmtp/rules` directory.

Please refer to the [dedicated chapter guide on the `vSL`](../reference/vSL/vsl.md) for further details.

&#9758; | The vSMTP service must be restarted to apply changes.

## The `vsmtp.service` file

This file contains all the mandatory information to start the vSMTP service on Linux server using [systemd] as the system and service manager.

[systemd]: https://freedesktop.org/wiki/Software/systemd/

&#9762; | Do not modify this file unless being highly aware of the impacts of your changes.
