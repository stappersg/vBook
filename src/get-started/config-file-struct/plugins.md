# Plugins

Plugins are dynamic libraries (`.so`) that can be imported by `.vsl` scripts.
They are bridges between third-party software (MySQL databases, an antivirus, redis databases, etc.) that uses `vSL` to interface with vSMTP and leverage filtering.

Plugins are placed in the `/usr/lib/vsmtp/` directory, and referenced in the configuration using symbolic links.

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
 ┃        ┣ config.vsl
 ┃        ┣ incoming.vsl
 ┃        ┣ outgoing.vsl
 ┃        ┗ internal.vsl
 ┣ domain-enabled/
 ┃    ┗ example.com -> /etc/vsmtp/domain-available/example.com
 ┣ objects/
 ┃    ┗ net.vsl
 ┣ services/
 ┗ plugins/
+     ┗ vsmtp-plugin-mysql.so -> /usr/lib/vsmtp/libvsmtp-plugin-mysql-1.0.0.so
```
<p class="ann"> Adding plugins and associated services </p>

They are then imported in "services", `.vsl` scripts that configure and use plugins features.

> Check out the [Plugin chapter](../../plugins/plugins.md) for more information.
