# Filtering

It is possible to filter emails using `.vsl` files for specific domains.

```diff
/etc/vsmtp
  ┣ vsmtp.vsl
  ┣ conf.d/
  ┃     ┣ config.vsl
  ┃     ┣ interfaces.vsl
  ┃     ┗ app.vsl
+ ┣ domain-available/
+ ┗ domain-enabled/
+        ┗ incoming.vsl
```

For vSMTP to take a rule path into account, you have to change the configuration in `conf.d/config.vsl` like so:

```rust
fn on_config(config) {
  config.app.vsl.dirpath = "/etc/vsmtp/domain-enabled";
  return config;
}
```

<p style="text-align: center;"> <i>Specifying filtering rules directory in the configuration</i> </p>

## Incoming

The root `incoming.vsl` script is used to filter incoming transaction at the `connect`, `helo` and `authenticate` stages of an SMTP transaction. (Check out the [Transaction Context](/ref/vSL/transaction.md) chapter for more details)

> If this script is not present in the directory configured by `config.app.vsl.dirpath`, vSMTP will deny all incoming transactions.

## Domains

In the rule directory, all sub-directories are considered as domains with rules applied to them.

```diff
/etc/vsmtp
  ┣ vsmtp.vsl
  ┣ conf.d/
  ┃     ┣ config.vsl
  ┃     ┣ interfaces.vsl
  ┃     ┗ app.vsl
  ┣ domain-available/
+ ┃     ┗ example.com
+ ┃          ┣ incoming.vsl
+ ┃          ┣ outgoing.vsl
+ ┃          ┗ internal.vsl
  ┗ domain-enabled/
        ┗ incoming.vsl
```

<p style="text-align: center;"> <i>Adding filtering for the `example.com` domain</i> </p>

vSMTP has been configured to pickup filtering rules in the `domain-enabled` directory. You will have to use symbolic links for vSMTP to use the scripts inside the `domain-available/example.com` directory.

```diff
/etc/vsmtp
  ┣ vsmtp.vsl
  ┣ conf.d/
  ┃     ┣ config.vsl
  ┃     ┣ interfaces.vsl
  ┃     ┗ app.vsl
  ┣ domain-available/
  ┃     ┗ example.com
  ┃          ┣ incoming.vsl
  ┃          ┣ outgoing.vsl
  ┃          ┗ internal.vsl
  ┗ domain-enabled/
        ┣ incoming.vsl
+       ┗ example.com -> /etc/vsmtp/domain-available/example.com
```

<p style="text-align: center;"> <i>Using symlinks to enable filtering for the `example.com` domain</i> </p>

> This directory structure is standard. The goal here is to disable / enable domain specific filtering by simply removing / adding symbolic links while keeping your configuration intact.

The server will pickup the scripts defined in the `domain-enabled/example.com` directory and run them following the conditions defined in the [Transaction Context chapter](/ref/vSL/transaction.md).

## Domain specific configuration

It is possible to add a specific configuration for each domain.

```diff
/etc/vsmtp
  ┣ vsmtp.vsl
  ┣ conf.d/
  ┃     ┣ config.vsl
  ┃     ┣ interfaces.vsl
  ┃     ┗ app.vsl
  ┣ domain-available/
  ┃     ┗ example.com
+ ┃         ┣ config.vsl
  ┃         ┣ incoming.vsl
  ┃         ┣ outgoing.vsl
  ┃         ┗ internal.vsl
  ┗ domain-enabled/
        ┗ incoming.vsl
        ┗ example.com -> /etc/vsmtp/domain-available/example.com
```

<p style="text-align: center;"> <i>Adding specific configuration for a domain</i> </p>

The `config.vsl` script under a domain must contain, at least, the following statement:

```rust
fn on_domain_config(config) {
  config
}
```

Like the root `config.vsl` file, this script contains a callback used to configure the domain. You can configure TLS, DKIM and DNS per domain.

```rust
fn on_domain_config(config) {
  config.tls = #{
    protocol_version: ["TLSv1.2", "TLSv1.3"],
    certificate: "/etc/vsmtp/certs/cert.pem",
    private_key: "/etc/vsmtp/certs/privkey.pem",
  };

  config.dkim = #{
    private_key: "/etc/vsmtp/certs/example.dkim.key",
  };

  config.server.dns.type = "system";

  config
}
```

<p style="text-align: center;"> <i>Changing TLS, DKIM and DNS parameters for a specific domain</i> </p>

> If this script is not present in a domain directory, configuration from the root `config.vsl` script is used instead.
