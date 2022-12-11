# Root configuration

By default, the following files are created in the `/etc/vsmtp` directory once vSMTP is installed.

```
/etc/vsmtp
┣ vsmtp.vsl
┗ conf.d/
      ┗ config.vsl
```

`vsmtp.vsl` is the mandatory entrypoint for vSMTP. It's content SHOULD NOT be modified, since it can change between versions.

`conf.d/config.vsl`, on the other hand, is a mandatory configuration file that contains the root configuration for vSMTP. To change the configuration, you will need to edit it.

This file must at least contain the following statement:

```rust
fn on_config(config) {
  return config;
}
```

vSMTP calls the `on_config` function once starting up. You are free to modify the `config` object to change the configuration. The `config` object MUST be returned at the end of the function.

> The [Configuration reference](../../ref/vSL/api/var::cfg.md) lists all fields that you can change in the `config` object.

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

<p class="ann"> <i>Configuring vSMTP with `conf.d/config.vsl`</i> </p>

## Recommandations

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

<p class="ann"> <i>/etc/vsmtp/conf.d/interfaces.vsl</i> </p>

and:

```rust
// The folder containing filtering rules.
export const rules_dirpath = "/etc/vsmtp/domain-enabled";
```

<p class="ann"> <i>/etc/vsmtp/conf.d/app.vsl</i> </p>

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

<p class="ann"> <i>/etc/vsmtp/conf.d/config.vsl</i> </p>