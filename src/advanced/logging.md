# Logging

The vSMTP logging subsystem include syslog, server logs, and application logs.

## Server logs

Server logs concerns the vSMTP server and include information about the client, the internal state, etc.

The default output directory is `/var/log/vsmtp/vsmtp.log`.

Logs are configured by "modules", that represent a specific part of the server.
The `rule_engine` module enables logs for the rule engine, the `parser` module for the
mime parser, etc.

The `vsmtp.toml` file is used to configure server logs, such as below:

```toml
[server.logs]
# You can change the location of the server logs.
filepath = "./tmp/system/vsmtp.log"

level = [
    # set global logging to "info", set the same log level for all modules.
    "default=info",

    # set specific vSMTP module logs (override "server" log level for specific module)
    # possible modules are:
    #   - queue
    #   - receiver
    #   - rule_engine
    #   - delivery
    #   - parser
    #   - runtime
    #   - processes
    "receiver=info",
    "rule_engine=warn",
    "delivery=error",
    "parser=trace",
]
```

## Application logs

Application logs are defined using the `log(level, message)` function in the vSL rules.

The default output location can be modified in the `vsmtp.toml` file, using this directive:

```toml
[app.logs]
# You can change the location of the application logs.
filepath = "./tmp/system/app.log"
```

## Syslog

vSMTP automatically send logs to the syslog daemon using the `mail` category and the `info` level. It is not yet configurable.
