# Filtering

It is possible to filter emails using `.vsl` files for incoming emails and specific domains. `vSL` is the `vSMTP scripting language`, a superset of [Rhai](https://rhai.rs/) which is used to filter emails, modify their contents, send them to a specific target, etc.

> The [vSL chapter](../../filtering/vsl.md) explains in detail what is possible to do with `.vsl` scripts.

## Root Filter

The root `filter.vsl` script is used to filter incoming transaction at the `connect`, `helo` and `authenticate` stages of an SMTP transaction. (Check out the [Transaction Context](../../filtering/transaction.md) chapter for more details)

```diff
/etc/vsmtp
 ┣ vsmtp.vsl
+┣ filter.vsl
 ┣ conf.d/
 ┃    ┣ config.vsl
 ┃    ┣ interfaces.vsl
 ┃    ┗ app.vsl
 ┣ domain-available/
 ┣ domain-enabled/
 ┣ objects/
 ┣ services/
 ┗ plugins/
```
<p class="ann"> Adding the root filter script </p>

```rust,ignore
fn on_config(config) {
  config.app.vsl.filter_path = "/etc/vsmtp/filter.vsl";
  return config;
}
```
<p class="ann"> Specifying the path to the filter in the configuration </p>

> If this script is not present, vSMTP will deny all incoming transactions by default.

## Domains

It is also possible to filter emails per domain.

```diff
 ┣ vsmtp.vsl
 ┣ filter.vsl
 ┣ conf.d/
 ┃    ┣ config.vsl
 ┃    ┣ interfaces.vsl
 ┃    ┗ app.vsl
 ┣ domain-available/
+┃     ┗ example.com/
+┃          ┣ incoming.vsl
+┃          ┣ outgoing.vsl
+┃          ┗ internal.vsl
 ┣ domain-enabled/
 ┣ objects/
 ┣ services/
 ┗ plugins/
```
<p class="ann"> Adding filtering scripts for the `example.com` domain under the `domain-available` directory </p>

The configuration in `conf.d/config.vsl` must be updated like so:

```rust,ignore
fn on_config(config) {
  config.app.vsl.domain_dir = "/etc/vsmtp/domain-enabled";

  return config;
}
```
<p class="ann"> Specifying filtering rules directory for domains in the configuration </p>

In the above configuration, vSMTP has been setup to pickup filtering rules in the `domain-enabled` directory, not `domain-available`. You will have to use symbolic links for vSMTP to use the scripts inside the `domain-available/example.com` directory.

```diff
/etc/vsmtp
 ┣ vsmtp.vsl
 ┣ filter.vsl
 ┣ conf.d/
 ┃    ┣ config.vsl
 ┃    ┣ interfaces.vsl
 ┃    ┗ app.vsl
 ┣ domain-available/
 ┃    ┗ example.com/
 ┃         ┣ incoming.vsl
 ┃         ┣ outgoing.vsl
 ┃         ┗ internal.vsl
 ┣ domain-enabled/
+┃    ┗ example.com -> /etc/vsmtp/domain-available/example.com
 ┣ objects/
 ┣ services/
 ┗ plugins/
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
 ┃    ┣ config.vsl
 ┃    ┣ interfaces.vsl
 ┃    ┗ app.vsl
 ┣ domain-available/
 ┃    ┗ example.com
+┃        ┣ config.vsl
 ┃        ┣ incoming.vsl
 ┃        ┣ outgoing.vsl
 ┃        ┗ internal.vsl
 ┣ domain-enabled/
 ┃    ┗ example.com -> /etc/vsmtp/domain-available/example.com
 ┣ objects/
 ┣ services/
 ┗ plugins/
```

<p class="ann"> Adding specific configuration for a domain </p>

The `config.vsl` script under a domain must contain, at least, the following statement:

```rust,ignore
fn on_domain_config(config) {
  config
}
```
<p class="ann"> An empty domain specific configuration </p>

Like the root `config.vsl` file, this script contains a function used to configure the domain, in this case called `on_domain_config`. You can configure TLS, DKIM and DNS for each domain.

```rust,ignore
fn on_domain_config(config) {
  config.tls = #{
    protocol_version: ["TLSv1.2", "TLSv1.3"],
    certificate: "/etc/vsmtp/certs/fullchain.pem",
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
