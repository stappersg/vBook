# Plugins

vSMTP feature set can be extended using plugins.

Plugins are dynamic libraries (`.so` files on Linux) that exposes `vSL` interfaces and are used during filtering.

## Recommandation

### Plugin directory

A plugin should be accessible in a `plugins` directory in your configuration.

```diff
/etc/vsmtp
  ┣ vsmtp.vsl
  ┃ conf.d/
  ┃  ┗ ...
+ ┗ plugins
+    ┣ lib-plugin.so
+    ┗ ...
```

To make things cleaner with Linux's file system, it is recommended that you store plugins in the `/usr/lib/vsmtp` directory, and use symbolic links to those libraries in the plugins folder.

```diff
/etc/vsmtp
  ┣ vsmtp.vsl
  ┃ conf.d/
  ┃  ┗ ...
+ ┗ plugins
+    ┣ lib-plugin.so -> /usr/lib/vsmtp/lib-plugin.so
+    ┗ ...
```

```sh
ln -s /usr/lib/vsmtp/lib-plugin.so /etc/vsmtp/plugins/lib-plugin.so
```

### Services directory

Some plugins create Rhai objects that use system resources like sockets or file descriptors.
Constructing an instance of those objects can be costly.

Thus, it is HIGHLY recommended that objects created by plugins are declared inside `.vsl` files stored in the `/etc/vsmtp/services` directory. This way objects are initialized only once when vSMTP starts.

Here is an example:

```diff
/etc/vsmtp
  ┣ vsmtp.vsl
  ┣ conf.d/
  ┃     ┗ config.vsl
  ┣ domain-available/
  ┃     ┗ example.com/
  ┃       ┗ ...
  ┣ domain-enabled/
  ┃     ┣ incoming.vsl
  ┃     ┗ example.com -> ...
+ ┗ services/
+       ┗ command.vsl
```

```rust,ignore
// Do not forget to use the `export` keyword when declaring
// the object to make it accessible trough `import`.
const echo = cmd(#{
    command: "echo",
    args: [ "-n", "executing a command from vSMTP!" ],
});
```

<p class="ann"> Creating a new command object in `services/command.vsl` </p>

> Check out the [Command](../ref/command.md) reference to get examples for the command plugin.

```rust,ignore
import "services/command" as command;

#{
  connect: [
    action "use echo" || command::echo.run(),
  ]
}
```

<p class="ann"> Using the object in rules using Rhai's import statement </p>
