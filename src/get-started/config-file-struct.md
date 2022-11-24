# Configuring vSMTP

vSMTP, by default, stores it's configuration in `/etc/vsmtp`. Lets look at how files are organized.

## Overview

A typical vSMTP configuration looks like the following.

```
/etc/vsmtp
┣ vsmtp.vsl
┣ conf.d/
┃     ┣ config.vsl
┃     ┗ *.vsl
┣ domain-available/
┃     ┣ example.com/
┃     ┃    ┣ config.vsl
┃     ┃    ┣ incoming.vsl
┃     ┃    ┣ outgoing.vsl
┃     ┃    ┗ internal.vsl
┃     ┗ test.com/
┃         ┗ ...
┣ domain-enabled/
┃     ┣ incoming.vsl
┃     ┗ example.com -> /etc/vsmtp/domain-available/example.com
┣ services/
┃     ┣ users-ldap.vsl
┃     ┣ backup-mysql.vsl
┃     ┗ *.vsl
┣ objects/
┃     ┣ net.vsl
┃     ┗ *.vsl
┗ plugins/
      ┣ mysql -> /usr/lib/vsmtp/libvsmtp-mysql-plugin.so
      ┗ ldap  -> /usr/lib/vsmtp/libvsmtp-ldap-plugin.so
```

Lets break it down step by step, by building a configuration from scratch.

### Root configuration

In `/etc/vsmtp`, by default, the following is created by vSMTP once installed.

```
/etc/vsmtp
┣ vsmtp.vsl
┗ conf.d/
      ┗ config.vsl
```

`vsmtp.vsl` is the mandatory entrypoint for vSMTP, you SHOULD NOT change any of it's content, since maintainers of the program will edit it following new updates.

`conf.d/config.vsl`, on the other hand, is a mandatory configuration file that contains the root configuration for vSMTP. To change the configuration, you will need to edit it.

This file must at least contain the following statement:

```rust
fn on_config(config) {
  return config;
}
```

vSMTP calls the `on_config` function once starting up. You are free to modify the `config` object to change the configuration. The `config` object MUST be returned at the end of the function.

> The [Configuration reference](/src/reference/config-file.md) lists all fields that you can change in the `config` object.

For example:
```rust
fn on_config(config) {
  // Change the name of the server.
  config.server.name = "example.com";

  // Specify addresses that the server will listen to.
  config.server.interfaces = #{
    addr: ["192.168.1.254:25"],
    addr_submission: ["192.168.1.254:587"],
    addr_submissions: ["192.168.1.254:465"],
  };

  // Change the folder containing filtering rules.
  config.app.vsl.dirpath = "/etc/vsmtp/domain-enabled";

  return config;
}
```
<p style="text-align: center;"> <i>Configuring vSMTP with `conf.d/config.vsl`</i> </p>

#### Recommandations

Rhai exposes a [module API](https://rhai.rs/book/language/modules/index.html), making it possible to split the configuration by theme.

For the above example, it is recommended that configuration files are split this way:
```diff
/etc/vsmtp
 ┣ vsmtp.vsl
 ┗ conf.d/
       ┣ config.vsl
+      ┣ interfaces.vsl
+      ┗ app.vsl
```

with:
```rust
// addresses that the server will listen to.
export const interfaces = #{
  addr: ["192.168.1.254:25"],
  addr_submission: ["192.168.1.254:587"],
  addr_submissions: ["192.168.1.254:465"],
};
```
<p style="text-align: center;"> <i>/etc/vsmtp/conf.d/interfaces.vsl</i> </p>

and:
```rust
// The folder containing filtering rules.
export const rules_dirpath = "/etc/vsmtp/domain-enabled";
```
<p style="text-align: center;"> <i>/etc/vsmtp/conf.d/app.vsl</i> </p>

Those modules can then be imported in `config.vsl`, resulting in a more cleaner configuration file.

```rust
import "conf.d/interfaces" as i;
import "conf.d/app" as app;

fn on_config(config) {
  config.server.name = "example.com";
  config.server.interfaces = i::interfaces;
  config.app.vsl.dirpath = app::rules_dirpath;

  return config;
}
```
<p style="text-align: center;"> <i>/etc/vsmtp/conf.d/config.vsl</i> </p>

### Filtering

It is possible to filter emails using `.vsl` files for specific domains.

```diff
/etc/vsmtp
  ┣ vsmtp.vsl
  ┣ conf.d/
  ┃     ┣ config.vsl
  ┃     ┣ interfaces.vsl
  ┃     ┗ app.vsl
+ ┗ domain-available/
+ ┣ domain-enabled/
+ ┃       ┗ incoming.vsl
```

For vSMTP to take a rule path into account, you have to change the configuration in `conf.d/config.vsl` like so:
```rust
fn on_config(config) {
  config.app.vsl.dirpath = "/etc/vsmtp/domain-enabled";
  return config;
}
```
<p style="text-align: center;"> <i>Specifying filtering rules directory in the configuration</i> </p>

#### incoming

The root `incoming.vsl` script is is used to filter incoming transaction at the `connect`, `helo` and `authenticate` stages of an SMTP transaction. (Check out the [Transaction Context](/src/reference/vSL/transaction.md) chapter for more details)

#### Sub domains

In the rule directory, all sub-directories are considered as subdomains with rules applied to them.

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
<p style="text-align: center;"> <i>Adding filtering for a sub-domain</i> </p>

Here, an `example.com` folder has been added.

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

> Using this architecture is NOT MANDATORY. You could simply set the `config.app.vsl.dirpath` configuration variable to `/etc/vsmtp/domain-available`. The goal here is to disable / enable domain specific filtering by simply removing / adding symbolic links while keeping your configuration intact.

The server will pickup the scripts defined in the `example.com` folder and run them following the conditions defined in the [Transaction Context](/src/reference/vSL/transaction.md) chapter.

#### Sub domain specific configuration

It is possible to add a specific configuration for each sub domain. 

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
<p style="text-align: center;"> <i>Adding specific configuration for a sub-domain</i> </p>

The `config.vsl` script under a sub domain must contain, at least, the following statement:

```rust
fn on_domain_config(config) {
  config
}
```

As the root `config.vsl` file, this script contains a callback used to configure the sub domain. You can configure TLS, DKIM and DNS per sub-domain.

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
<p style="text-align: center;"> <i>Changing TLS, DKIM and DNS parameters for a specific sub-domain</i> </p>

> If this script is not present in a subdomain, configuration from the root `config.vsl` script is used instead.