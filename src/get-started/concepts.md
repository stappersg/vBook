# Concepts

## Configuration

vSMTP is a server that does not use a traditional configuration language to configure itself: it uses `.vsl` files (vSMTP Scripting Language) that are scripts based on the [Rhai programming language](https://rhai.rs/) with additionnal functions and syntax on top of it.

## Filtering

SMTP filtering is performed by a rule engine, which uses `.vsl` scripts to filter any incoming connection, email, user etc ...

Its syntax is similar to a configuration format, but with programmatic capabilities. It is based on two filtering primitives: `rules` and `actions`.

Please refer to the dedicated chapter guide on [vSL](/ref/vSL/vsl.md) for further details.

## Service configuration

The `vsmtp.service` file contains all the mandatory information to start the vSMTP service on Linux server using [systemd] as the system and service manager.

[systemd]: https://freedesktop.org/wiki/Software/systemd/
