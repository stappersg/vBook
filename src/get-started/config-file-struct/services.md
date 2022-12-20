# Services

Services are a standard way to configure and use plugins enabled in the `plugins` directory. 

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
+┃    ┗ mysql-service.vsl
 ┗ plugins/
      ┗ vsmtp-plugin-mysql.so -> /usr/lib/vsmtp/libvsmtp-plugin-mysql-1.0.0.so
```

Declared as `.vsl` scripts, they expose variables or functions that uses plugins interfaces.

For example, a MySQL plugin is available to download, we can use it's interface inside of a service script called `mysql-service.vsl`.

```rust,ignore
import "plugins/vsmtp-plugin-mysql" as mysql;

// Let's establish a connexion to a MySQL database.
export const database = mysql::connect(...);
```
<p class="ann"> /etc/vsmtp/services/mysql-service.vsl </p>

> Check out the [MySQL plugin tutorial](../../plugins/mysql.md) for more details.