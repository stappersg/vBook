# Concepts

vSMTP is a server that does not use a traditional configuration language to configure itself: it uses `.vsl` files (vSMTP Scripting Language) that are scripts based on the [Rhai programming language](https://rhai.rs/) with features on top of it.

## Configuration

vSMTP is configured with `.vsl` files. More on that in the next chapter.

## Filtering

SMTP filtering is performed by a rule engine, which uses `.vsl` scripts to filter any incoming connection, email, user etc ...

Its syntax is similar to a configuration format, but with programmatic capabilities. It is based on two filtering primitives: `rules` and `actions`.

Please refer to the dedicated chapter guide on [vSL](../reference/vSL/vsl.md) for further details.

## Service configuration

The `vsmtp.service` file contains all the mandatory information to start the vSMTP service on Linux server using [systemd] as the system and service manager.

[systemd]: https://freedesktop.org/wiki/Software/systemd/

# TODO: OLD, TO REMOVE

## System configuration

The behavior of the vSMTP service (network, default directories, tls, etc.) can be configured by editing the `vsmtp.vsl` file. Its default location is `/etc/vsmtp/vsmtp.vsl`.

When starting the vSMTP service, its configuration file is read and fully parsed. An error occurs when a key or a value is incorrect. The server never crashes if the configuration is successfully loaded.

Please refer to the [vSMTP vsl config key/value list](../reference/config-file.html) chapter for further details.

## Application configuration

SMTP filtering is performed by a rule engine. Scripts are written in simple, but powerful, programming language : vSMTP Scripting Language (vSL). The entry point is the `main.vsl` file.

Its syntax is similar to a configuration format, but with programmatic capabilities. It is based on four main concepts : `rules`, `actions`, `objects` and `services`.

Please refer to the dedicated chapter guide on [vSL](../reference/vSL/vsl.md) for further details.

## Service configuration

The `vsmtp.service` file contains all the mandatory information to start the vSMTP service on Linux server using [systemd] as the system and service manager.

[systemd]: https://freedesktop.org/wiki/Software/systemd/
