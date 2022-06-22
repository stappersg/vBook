# Logging

By default, logs are located at `/var/log/vsmtp/vsmtp.log`.

Logs are configured by "modules", that represent a specific part of the server.
The `rule_engine` module will enable logs for the rule engine, `parser` for the
mime parser, etc ...

To configure logs, use the syntax down below:

```toml
[server.logs]
# You can change the location of the server logs.
filepath = "./tmp/system/vsmtp.log"
# You can change de message format of the logs.
# See https://docs.rs/log4rs/latest/log4rs/encode/pattern/index.html#formatters
# for available formatters.
format = "{d} - {m}{n}"
# Maximum size in bytes of a log file. (default 10M)
size_limit = 10_485_760
# Maximum number of archive kept, the excess is deleted. (default 10)
archive_count = 20

[server.logs.level]
# enable logging from vSMTP dependencies.
root = "warn"
# set global logging to "info", set the same log level for all modules.
server = "info"
# set specific vSMTP module logs (override "server" log level for specific module)
# possible modules are:
#   - queue
#   - receiver
#   - rule_engine
#   - rule_engine
#   - delivery
#   - parser
#   - runtime
#   - processes
receiver = "trace"
rule_engine = "trace"
``` 