# Logging

In vSMTP, logs are separated in two categories: server logs & app logs.

* server logs are relative to vsmtp, they regroup information about the client, internal state & errors.
* app logs are written using the `log(level, message)` function in your `vsl` rules.

## Server logs

By default, server logs are located at `/var/log/vsmtp/vsmtp.log`.

Logs are configured by "modules", that represent a specific part of the server.
The `rule_engine` module will enable logs for the rule engine, `parser` for the
mime parser, etc ...

To configure server logs, use the syntax down below in your `vsmtp.toml`:

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

To configure applicative logs (log output of your vsl files, using the `log(level, message)` function), write the following in your `vsmtp.toml`:

```toml
[app.logs]
# You can change the location of the application logs.
filepath = "./tmp/system/app.log"
```

## Syslogs

vSMTP automatically write to syslogs with the `info` level by default. It is not yet configurable.
Files are written at `/dev/log` or `/var/run/syslog`.