# Root configuration

By default, the following files are created in the `/etc/vsmtp` directory once vSMTP is installed.

```
/etc/vsmtp
┣ vsmtp.vsl
┣ conf.d/
┃      ┗ config.vsl
┣ domain-available/
┣ domain-enabled/
┣ objects/
┣ services/
┗ plugins/
```
<p class="ann"> Default file structure in `/etc/vsmtp`</p>

`vsmtp.vsl` is the mandatory entrypoint for vSMTP. It's content SHOULD NOT be modified, since it can change between versions.

`conf.d/config.vsl`, on the other hand, is a mandatory configuration file that contains the root configuration for vSMTP.

This file must at least contain the following statement:

```rust,ignore
fn on_config(config) {
  return config;
}
```
<p class="ann"> An empty root configuration file in `/etc/vsmtp/conf.d/config.vsl`</p>

vSMTP calls the `on_config` function once starting up. Modify the `config` object to change the configuration. The `config` object MUST be returned at the end of the function.

> The [Configuration reference](../../ref/vSL/api/var::cfg.md) lists all fields that can be changed in the `config` object.

For example:

```rust,ignore
fn on_config(config) {
  // Change the name of the server.
  config.server.name = "example.com";

  // Specify addresses that the server will listen to.
  config.server.interfaces = #{
    addr: ["192.168.1.254:25"],
    addr_submission: ["192.168.1.254:587"],
    addr_submissions: ["192.168.1.254:465"],
  };

  // Specify a user and group that will run vsmtp.
  // If those fields are not set, vsmtp will try to use,
  // by default, the `vsmtp` user and `vsmtp` group.
  config.server.system = #{
    user: "debian-1",
    group: "mail",
  };

  // Change filter rules locations.
  config.app.vsl.filter_path = "/etc/vsmtp/filter.vsl";
  config.app.vsl.domain_dir = "/etc/vsmtp/domain-enabled";

  return config;
}
```

<p class="ann"> Configuring vSMTP by changing the `config` object </p>

> It is recommended that you use absolute paths in your configuration files. Relative paths will be relative to the execution path of vSMTP.

## Splitting configuration in modules

Rhai exposes a [module API](https://rhai.rs/book/language/modules/index.html), making it possible to split the configuration by theme.

For example, it is possible to split the above configuration this way:

```diff
/etc/vsmtp
 ┣ vsmtp.vsl
 ┣ conf.d/
 ┃    ┣ config.vsl
+┃    ┣ interfaces.vsl
+┃    ┗ app.vsl
 ┣ domain-available/
 ┣ domain-enabled/
 ┣ objects/
 ┣ services/
 ┗ plugins/
```
<p class="ann"> Adding modules to split the configuration </p>

Let's define the addresses that the server will listen to.

```rust,ignore
export const interfaces = #{
  addr: ["192.168.1.254:25"],
  addr_submission: ["192.168.1.254:587"],
  addr_submissions: ["192.168.1.254:465"],
};
```
<p class="ann"> `/etc/vsmtp/conf.d/interfaces.vsl` </p>

Let's also write our filtering scripts locations.

```rust,ignore
// Filter by domain.
export const domain_dir = "/etc/vsmtp/domain-enabled";
// Global filter.
export const filter_path = "/etc/vsmtp/filter.vsl";
```
<p class="ann"> `/etc/vsmtp/conf.d/app.vsl` </p>

Those modules can then be imported in `config.vsl`, resulting in a more cleaner configuration file.

```rust,ignore
import "conf.d/interfaces" as i;
import "conf.d/app" as app;

fn on_config(config) {
  config.server.name = "example.com";
  config.server.interfaces = i::interfaces;

  config.server.system = #{
    user: "debian-1",
    group: "mail",
  };

  config.app.vsl.domain_dir = app::domain_dir;
  config.app.vsl.filter_path = app::filter_path;

  return config;
}
```
<p class="ann"> `/etc/vsmtp/conf.d/config.vsl` </p>