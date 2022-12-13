# Plugins

Plugins are dynamic libraries (`.so`) that can be imported by `.vsl` scripts.
They are bridges between third-party software (MySQL databases, an antivirus, redis databases, etc) that uses `vSL` to interface with vSMTP and leverage filtering.

Plugins are placed in the `/usr/lib/vsmtp/` directory, and referenced in the configuration using symbolic links.

```diff
  /etc/vsmtp
  ┣ vsmtp.vsl
  ┣ filter.vsl
  ┣ conf.d/
  ┃     ┣ config.vsl
  ┃     ┗ *.vsl
  ┣ domain-available/
  ┃     ┗ example.com/
  ┃         ┗ ...
  ┣ domain-enabled/
  ┃     ┗ example.com -> /etc/vsmtp/domain-available/example.com
  ┣ objects/
  ┃     ┣ net.vsl
  ┃     ┗ *.vsl
+ ┣ services/
+ ┃     ┣ my_plugin.vsl
+ ┃     ┗ *.vsl
+ ┗ plugins/
+   ┣ my_plugin.so -> /usr/lib/vsmtp/libmy_plugin.so
+   ┗ ... 
```
<p class="ann"> Adding plugins and associated services </p>

They are then imported in "services", `.vsl` scripts that configure and use plugins features.

```rust,ignore
import "plugins/my_plugin" as my_plugin;

export const my_plugin_service = my_plugin::do_stuff();
```
<p class="ann"> `/etc/vsmtp/services/my_plugin.vsl` </p>

Services can be used during filtering, after being imported like an object.

> Check out the [Plugin chapter](../../plugins/plugins.md) for more information.