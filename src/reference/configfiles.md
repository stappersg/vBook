## vSMTP configuration files

vSMTP and its sub-systems use [TOML] language for their configuration files. TOML files are frequently compared to INI for their similarities in syntax and use as configuration files.

[TOML]: https://toml.io/

TOML uses tables (hash tables) as collections of key/value pairs. Key/value pairs within tables are not guaranteed to be in any specific order. Tables appear in square brackets on a line by themselves. Dots are used to signify nested tables. Nested array of tables are also allowed.

### The vsmtp.toml file

This is the main configuration file. It should be located in /etc/vsmtp. However it can be modified in the vSMTP service file.

| Table | Comment
| :--- | :---
| [server] | vSMTP overall configuration.
| [smtp] | Legacy IMF/SMTP transaction.
| [smtps] | TLS/SSL Encryption.
| [reply_codes] | User defined SMTP(s) reply codes.
| [rules] | vSL configuration.
| [logs] | Log level per subsystem, path, etc.
| [quarantine] | Behavior of the user defined quarantines.
| [delivery] | Delivery subsystem configuration, including deferred and dead queues.

Please refer to the vsmtp.default.toml file for a fully description of the key/value pairs.

### The vsmtp.service file

This file contains all the mandatory information to start the vSMTP service on Linux using [systemd] as the system and service manager.

[systemd]: https://freedesktop.org/wiki/Software/systemd/

```shell
[Unit]
Description=vSMTP Mail Transfer Agent
Conflicts=sendmail.service exim4.service postfix.service 
ConditionPathExists=/etc/vsmtp/vsmtp.toml
After=network-online.target 
Wants=network-online.target

[Service]
Type=simple
User=vsmtp
Group=vsmtp
AmbientCapabilities=CAP_NET_BIND_SERVICE
UMask=007
ExecStart=/usr/sbin/vsmtp -c /etc/vsmtp/vsmtp.toml
Restart=on-failure
TimeoutStopSec=300

[Install]
WantedBy=multi-user.target
```

&#9762; | Do not modify this file unless you know what you are doing. Please note that version 0.10 comes with a new startup mechanism.
