# Filtering

It is possible to filter emails using `.vsl` files for specific domains.

```diff
/etc/vsmtp
  ┣ vsmtp.vsl
+ ┣ filter.vsl
  ┣ conf.d/
  ┃     ┣ config.vsl
  ┃     ┣ interfaces.vsl
  ┃     ┗ app.vsl
+ ┣ domain-available/
+ ┗ domain-enabled/
```
<p class="ann"> Adding filters </p>

To filter emails per domain, you have to change the configuration in `conf.d/config.vsl` like so:

```rust,ignore
fn on_config(config) {
  config.app.vsl.domain_dir = "/etc/vsmtp/domain-enabled";
  return config;
}
```
<p class="ann"> Specifying filtering rules directory in the configuration </p>

## Root Filter

The root `filter.vsl` script is used to filter incoming transaction at the `connect`, `helo` and `authenticate` stages of an SMTP transaction. (Check out the [Transaction Context](../../filtering/transaction.md) chapter for more details)

> If this script is not present in the directory configured by `config.app.vsl.filter_path`, vSMTP will deny all incoming transactions.

## Domains

In the rule directory, all sub-directories are considered as domains with rules applied to them.

```diff
/etc/vsmtp
  ┣ vsmtp.vsl
  ┣ filter.vsl
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
```

<p class="ann"> Adding filtering for the `example.com` domain </p>

vSMTP has been configured to pickup filtering rules in the `domain-enabled` directory. You will have to use symbolic links for vSMTP to use the scripts inside the `domain-available/example.com` directory.

```diff
/etc/vsmtp
  ┣ vsmtp.vsl
  ┣ filter.vsl
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
+       ┗ example.com -> /etc/vsmtp/domain-available/example.com
```

<p class="ann"> Using symlinks to enable filtering for the `example.com` domain </p>

> This directory structure is standard. The goal here is to disable / enable domain specific filtering by simply removing / adding symbolic links while keeping your configuration intact.

The server will pickup the scripts defined in the `domain-enabled/example.com` directory and run them following the conditions defined in the [Transaction Context chapter](../../filtering/transaction.md).

## Domain specific configuration

It is possible to add a specific configuration for each domain.

```diff
/etc/vsmtp
  ┣ vsmtp.vsl
  ┣ filter.vsl
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
        ┗ example.com -> /etc/vsmtp/domain-available/example.com
```

<p class="ann"> Adding specific configuration for a domain </p>

The `config.vsl` script under a domain must contain, at least, the following statement:

```rust,ignore
fn on_domain_config(config) {
  config
}
```
<p class="ann"> An empty domain specific configuration </p>

Like the root `config.vsl` file, this script contains a callback used to configure the domain. You can configure TLS, DKIM and DNS per domain.

```rust,ignore
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

<p class="ann"> Changing TLS, DKIM and DNS parameters for a specific domain </p>

> If this script is not present in a domain directory, configuration from the root `config.vsl` script is used instead.
