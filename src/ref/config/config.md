# Configuration Parameters

## `config.version_requirement`

Version of vSMTP to use, should not be changed.

```rust,ignore
fn on_config(config) {
    config.version_requirement = "1.0.0";
    config
}
```

## `config.path`

Path to the `vsmtp.vsl`, default to `/etc/vsmtp/vsmtp.vsl`.

```rust,ignore
fn on_config(config) {
    config.path = "/etc/vsmtp/vsmtp.vsl";
    config
}
```

## `config.server`

Configuration variables for the core of vSMTP.

## `config.server.name`

Name of the server. Used in return codes. Defaults to the hostname.

```rust,ignore
fn on_config(config) {
    config.server.name = "example.com";
    config
}
```

## `config.server.client_count_max`

Maximum number of clients that can connect at the same time. Defaults to 16.

```rust,ignore
fn on_config(config) {
    // Accept at maximum 100 clients at the same time.
    config.server.client_count_max = 100;
    // No limits.
    config.server.client_count_max = -1;
    config
}
```

## `config.server.message_size_limit`

Maximum authorized size for an email. Defaults to 10MB.

```rust,ignore
fn on_config(config) {
    // Max size is 20MB.
    config.server.message_size_limit = 20000000;
    config
}
```

## `config.server.interfaces`

Address served by `vSMTP`. Either ipv4 or ipv6.

```rust,ignore
fn on_config(config) {
    config.server.interfaces = #{
        addr: ["127.0.0.1:25", "127.0.0.1:10025"],
        addr_submission: ["127.0.0.1:587"],
        addr_submissions: ["127.0.0.1:465"],
    };

    config
}
```

## `config.server.system`

System configuration for the server.

If `config.server.system.user` and `config.server.system.group` are not set in the configuration, vSMTP will try to use, by default, the `vsmtp` user and `vsmtp` group to run the server.

```rust,ignore
fn on_config(config) {
    config.server.system = #{
        user: "vsmtp",
        group: "mail",
        // User used when writing emails to disk using Maildir or Mbox.
        group_local: "mail",
        // Number of threads per vSMTP process.
        thread_pool: #{
            receiver: 6,
            processing: 6,
            delivery: 6,
        };
    };

    config
}
```

## `config.server.logs`

Log configuration for the server.

```rust,ignore
fn on_config(config) {
    config.server.logs = #{
        filename: "/var/log/vsmtp/vsmtp.log",
        level: ["info"],
    };

    config
}
```

## `config.server.logs.system`

Type of system logs to use.

An example using syslogd.
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
        // It is possible to use:
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

An example using journald.
```rust,ignore
fn on_config(config) {
    config.server.logs.system = #{
        level: "info",
        backend: "journald",
    };

    config
}
```

## `config.server.queues`

Configuration of mail queues of vSMTP.

```rust,ignore
fn on_config(config) {
    // The root directory for the queuer system.
    config.server.queues.dirpath = "/var/spool/vsmtp";
    // Size of the channel queue communicating the mails from the `receiver` pool to the `processing` pool.
    config.server.queues.working.channel_size = 32;
    config.server.queues.delivery = #{
        // Size of the channel queue communicating the mails from the `processing` pool to the `delivery` pool.
        channel_size: 32,
        // Maximum number of attempt to deliver the mail before being considered dead.
        deferred_retry_max: 100,
        // The mail in the `deferred` are resend in a clock with this period.
        deferred_retry_period: "5m",
    };

    config
}
```

## `config.server.tls`

TLS configuration for vSMTP.

```rust,ignore
fn on_config(config) {
    config.server.tls = #{
        // Ignore the client’s ciphersuite order.
        // Instead, choose the top ciphersuite in the server list which is supported by the client.
        preempt_cipherlist: false,
        // Timeout for the TLS handshake. Sends a timeout message to the client once reached.
        handshake_timeout: "200ms",
        protocol_version: "TLSv1.3",
        cipher_suite: "TLS13_AES_256_GCM_SHA384",
    }

    config
}
```

## `config.server.smtp`

SMTP protocol configuration for receivers of vSMTP.

```rust,ignore
fn on_config(config) {
    config.server.smtp = #{
        auth: #{
            // Some mechanisms are considered unsecure under non-TLS connections.
            // If `false`, the server will allow to use them even on clair connections.
            enable_dangerous_mechanism_in_clair: false,
            // List of mechanisms supported by the server.
            mechanisms: ["Plain", "Login", "CramMd5"],
            // If the AUTH exchange is canceled, the server will not consider the connection as closing,
            // increasing the number of attempt failed, until `attempt_count_max`, producing an error.
            attempt_count_max: 3,
        },
        error: #{
            // The delay used between each response, after `soft_count` errors.
            // Unused if `soft_count` is `-1`.
            delay: "5s",
            // The maximum number of errors before the client is disconnected.
            // `-1` to disable
            hard_count: 20,
            // The maximum number of errors before the client is delay between each response.
            // `-1` to disable
            soft_count: 10,
        },
        // Maximum number of recipients per email.
        rcpt_count_max: 1000,
        // Timeout configuration for each SMTP command.
        timeout_client: #{
            connect: "5m",
            data: "5m",
            helo: "5m",
            mail_from: "5m",
            rcpt_to: "5m",
        },
    },

    config
}
```

## `config.server.dns`

Configure the internal DNS of vSMTP.

```rust,ignore
fn on_config(config) {
    // Using the resolver of the system (/etc/resolv.conf).
    config.server.dns = #{
        "type": "system",
    }

    // Options available for the google, cloudflare and custom dns configurations.
    const options = #{
        // Specify the timeout for a request. Defaults to 5 seconds
        timeout: "5s",
        // Number of retries after lookup failure before giving up. Defaults to 2
        attempts: 2,
        // Rotate through the resource records in the response (if there is more than one for a given name)
        rotate: false,
        // Use DNSSec to validate the request
        dnssec: true,
        // The ip_strategy for the Resolver to use when lookup Ipv4 or Ipv6 addresses
        ip_strategy: "Ipv4Only" | "Ipv6Only" | "Ipv4AndIpv6" | "Ipv6thenIpv4" | "Ipv4thenIpv6",
        // Cache size is in number of records (some records can be large)
        cache_size: 32,
        // Check /ect/hosts file before dns requery (only works for unix like OS)
        use_hosts_file: false,
        // Number of concurrent requests per query
        // Where more than one nameserver is configured, this configures the resolver to send queries
        // to a number of servers in parallel. Defaults to 2; 0 or 1 will execute requests serially.
        num_concurrent_reqs: 2,
    };

    // Using the google DNS resolver.
    config.server.dns = #{
        "type": "google",
        options,
    }

    // Using the google DNS resolver.
    config.server.dns = #{
        "type": "cloudflare",
        options;
    }

    // Using a custom DNS resolver.
    config.server.dns = #{
        "type": "custom",
        config: #{
            // base search domain.
            domain: "example.com",
            // search domains.
            search: [],
        },
        options
    }

    config
}
```

## `config.app`

Configuration variables for the applicative side of vSMTP.

```rust,ignore
fn on_config(config) {
    config.app = #{
        // Path where custom quarantine queues will be stored.
        "dirpath": "/var/spool/vsmtp/app",
        "logs": #{
            // path to the log file generated by calling the `log` function
            // in `.vsl` scripts.
            "filename": "/var/log/vsmtp/app.log",
        },
        "vsl": #{
            // Path to the domain specific filtering directory.
            "domain_dir": "/etc/vsmtp/domain-enabled",
            // Path to the root filter script.
            "filter_path": "/etc/vsmtp/filter.vsl",
        },
    };

    config
}
```