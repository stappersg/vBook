# Logging

The logging system is backed by tokio tracing and piped to multiple 'subscriber' :

- [Logging](#logging)
  - [Backend logs](#backend-logs)
  - [Application logs](#application-logs)
  - [Journald](#journald)
  - [Syslogd](#syslogd)

## Backend logs

Backend logs concerns the vSMTP internals output.

The default output directory is `/var/log/vsmtp/vsmtp.log`.

Log levels can be configured by "modules", representing part of the server, using the `env_logger` syntax (see [docs.rs](https://docs.rs/tracing-subscriber/0.3.15/tracing_subscriber/struct.EnvFilter.html)).
The `vsmtp_rule_engine` module enables logs for the rule engine, the `vsmtp_mail_parser` module for the mime parser, etc.

The `vsmtp.vsl` file is used to configure server logs:

```rust
fn on_config(config) {
    // You can change the location of the server logs.
    config.server.logs.filepath = "./tmp/system/vsmtp.log";

    config.server.logs.level = [
        // set global logging level to "info" for all the modules.
        "info",
    
        // set the logging level per module.
        "vsmtp_server::receiver=info",
        "vsmtp_rule_engine=warn",
        "vsmtp_delivery=error",
    ];

    config
}

```

## Application logs

Application logs are written using the `log(level, message)` function in the vSL rules.

The default output location is the `/var/log/vsmtp/app`. It can be modified in the `config.vsl` file :

```js
fn on_config(config) {
    // You can change the location of the application logs.
    config.app.logs.filepath = "./tmp/system/app.log";

    config
}
```


## Journald

vSMTP send logs to the journald daemon :

```js
fn on_config(config) {
    // You can change the location of the application logs.
    config.server.logs.system = #{
        // write only the message of a specific level and more
        level: "info",
        backend: "journald",
    };

    config
}

```


## Syslogd

vSMTP send logs to the syslog daemon using the `mail` facility :

```js
fn on_config(config) {
    // You can change the location of the application logs.
    config.server.logs.system = #{
        // write only the message of a specific level and more
        level: "info",
        backend: "syslogd",
        // format used by the logger see https://www.rfc-editor.org/rfc/rfc3164 and https://www.rfc-editor.org/rfc/rfc5424
        format: "3164",
    
        socket: #{ type: "unix", path: "/dev/log" },
        // or
        socket: #{ type: "tcp", server: "127.0.0.1:601" },
        // or
        socket: #{ type: "udp", server: "127.0.0.1:514", local: "127.0.0.1:0" },
        // note: address can be ipv4 / ipv6
    };

    config
}
```