## vSMTP configuration files

vSMTP and its sub-systems use [TOML] language for their configuration files. TOML files are frequently compared to INI for their similarities in syntax and use as configuration files.

[TOML]: https://toml.io/

TOML uses tables (hash tables) as collections of key/value pairs. Key/value pairs within tables are not guaranteed to be in any specific order. Tables appear in square brackets on a line by themselves. Dots are used to signify nested tables. Nested array of tables are also allowed.

### The vsmtp.toml file

This is the main configuration file. It should be located in `/etc/vsmtp`. However it can be modified in the vSMTP service file.

| Table    | Comment                      |
| :------- | :--------------------------- |
| [server] | vSMTP overall configuration. |
| [app]    | Rule engine configuration.   |

The `[server]` table contains all the required information to start the vSMTP server and the root domain parameters.

Virtual domains can be configured under the root domain:

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

- Omitted: In this case, the default settings are applied. They can be retrieved with the `vsmtp config-show` command.
- Specified in primary domain: All virtual domains use these settings.
- Specific to a virtual domain.

Please refer to the reference guide for a fully description of the key/value pairs.

### The vsmtp.service file

This file contains all the mandatory information to start the vSMTP service on Linux using [systemd] as the system and service manager.

[systemd]: https://freedesktop.org/wiki/Software/systemd/

&#9762; | Do not modify this file unless you know what you are doing.