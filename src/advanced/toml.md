# vSMTP configuration files

The configuration files of vSMTP and its sub-systems are defined using the [TOML] language. 

[TOML]: https://toml.io/

TOML uses hash tables as collections of key/value pairs. Key/value pairs within tables are not supposed to be in any specific order. Tables appear in square brackets. Dots are used to signify nested tables. Nested array of tables are also allowed.

## The vsmtp.toml file

The `vsmtp.toml` is the main configuration file. It should be located in `/etc/vsmtp` directory. An alternative filename or location can be specified in the systemd's service file `/etc/systemd/system/vsmtp.service` or, in interactive mode, using the `--config` option.

The vSMTP TOML file is currently split into two main tables:

| Table    | Comment                      |
| :------- | :--------------------------- |
| [server] | The vSMTP overall configuration and its system interactions.|
| [app]    | The application configuration and the rule engine behavior.|

> Future releases may provide new tables.

The `[server]` table contains all the required information to start the vSMTP server and the root domain parameters.
As shown in the example below, virtual domains can be configured under the root domain.

```toml 
[server]
# system configuration
# 

#
# Root domain 
#
domain = "root-example.net"

[server.dns]
type = "google"

[server.tls]
security_level = "None"

# ...
# ... End of main domain configuration

#
# Virtual domain : "example1.com"
#
[server.virtual."example1.com"]
# DNS type is not specified - thus it's inherited from the main domain

[server.virtual."example1.com".tls]
protocol_version = "TLSv1.3"
certificate = "./certs/certificate-example1.crt"
private_key = "./certs/private-example2.key"

#
# Virtual domain : "example2.com"
#
[server.virtual."example2.com"]

[server.virtual."example2.com".dns]
type = "system"

[server.virtual."example2.com".tls]
protocol_version = "TLSv1.3"
certificate = "./certs/certificate-example2.crt"
private_key = "./certs/private-example2.key"
```

Parameters can be:

- Omitted: In this case, the default settings apply. They can be retrieved with the `vsmtp config-show` command.
- Specified in primary domain: All virtual domains use these settings.
- Specific to a virtual domain.

Please refer to the [reference guide] for a fully description of the key/value pairs.

[reference guide]: ../reference/config-file.md

## The vsmtp.service file

This file contains all the mandatory information to start the vSMTP service on Linux server using [systemd] as the system and service manager.

[systemd]: https://freedesktop.org/wiki/Software/systemd/

&#9762; | Do not modify this file unless being highly aware of the impacts of your changes.