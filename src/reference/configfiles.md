## vSMTP configuration files

vSMTP and its sub-systems use [TOML] language for their configuration files. TOML files are frequently compared to INI for their similarities in syntax and use as configuration files.

[TOML]: https://github.com/toml-lang/toml

TOML uses table (hash tables) as collections of key/value pairs. Key/value pairs within tables are not guaranteed to be in any specific order. Tables appear in square brackets on a line by themselves. Dots are used to signify nested tables. Nested array of tables are allowed.

vSMTP 

| Table | Comment
| :--- | :---
| [server] | vSMTP overall configuration
| [logs] | Logs
| [logs.level]

[smtp]
[smtp.error]

| [smtps] | SMTP secured transaction configuration
| [[smtps.sni_maps]]
[reply_codes]
| [rules]
[delivery]
[delivery.queues]

Please refer to the vsmtp.default.toml file for a fully description of the key/value pairs.
