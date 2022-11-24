# Plugins

vSMTP feature set can be extended using plugins.

Plugins are dynamic libraries (`.so` files on Linux) that exposes `vSL` interfaces and are used during filtering.

## Recommandation

A plugin should be placed in a `plugins` directory in your configuration.

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
