# Logging

Multiple log backends are available for vSMTP.

## vSMTP default logs

Default vSMTP log system. By default, it writes logs in the `/var/log/vsmtp/vsmtp.log` file.

```rust,ignore
fn on_config(config) {
    // You can change the location of the logs.
    config.server.logs.filename = "./tmp/system/vsmtp.log";
    // Set global logging level to "info".
    //
    // The configuration for the level here is an array because vSMTP
    // will support log levels for specific modules of the server in future releases.
    config.server.logs.level = [ "info" ];

    config
}
```
<p class="ann"> Configuring logs in the root configuration file </p>

## Application logs

Application logs are written using the `log(level, message)` function in filtering scripts.
The default output location is of application logs is the `/var/log/vsmtp/app.log` file. It can be changed in the root configuration.

```rust,ignore
fn on_config(config) {
    config.app.logs.filename = "./tmp/system/app.log";
    config
}
```
<p class="ann"> Change the location of the application logs. </p>

## System logs

vSMTP also supports system logs through the following services.

### Journald

vSMTP will send server logs to the journald daemon.

```rust,ignore
fn on_config(config) {
    config.server.logs.system = #{
        level: "info",
        backend: "journald",
    };

    config
}

```
<p class="ann"> Configure journald for vSMTP </p>


### Syslogd

vSMTP will send logs to the syslog daemon using the `mail` facility.

```rust,ignore
fn on_config(config) {
    config.server.logs.system = #{
        level: "info",
        backend: "syslogd",

        // Format used by the logger.
        // See https://www.rfc-editor.org/rfc/rfc3164 and https://www.rfc-editor.org/rfc/rfc5424
        // for more details.
        format: "3164",

        // Writing syslogs on disk using a unix socket.
        socket: #{ type: "unix", path: "/dev/log" },
        // You can also use:
        // `socket: #{ type: "tcp", server: "127.0.0.1:601" }`
        //
        // or
        // `socket: #{ type: "udp", server: "127.0.0.1:514", local: "127.0.0.1:0" }`
        //
        // note: address can be ipv4 / ipv6
    };

    config
}
```
<p class="ann"> Configure syslogs for vSMTP </p>

## Levels

|level|note|
|:-:|:-:|
|error| vSMTP encountered an issue, you should try to fix it or open an issue on vSMTP's repository. |
|warn| Something unexpected append, vSMTP will still run but you should look into it. |
|info| General informations on what the server is doing. |

<p class="ann"> Available log levels </p>

Debug and Trace levels are, for the time being, not available in the production version of vSMTP.