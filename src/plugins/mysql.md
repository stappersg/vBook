# MySQL

The mysql plugin lets you query mysql databases.

## Install

Install `libvsmtp_plugin_mysql.so` in `/usr/lib/vsmtp`, then use a symbolic link in your configuration.

```sh
ln -s /usr/lib/vsmtp/libvsmtp_plugin_mysql.so /etc/vsmtp/plugins/libvsmtp_plugin_mysql.so
```

## Using the plugin

```rust,ignore
import "plugins/libvsmtp_plugin_mysql" as db;

export const database = db::mysql(#{
    // the url to connect to your database.
    url: "mysql://localhost/",
    // the time allowed to the database to send a
    // response to your query. (optional, 30s by default)
    timeout: "30s",
    // the number of connections to open on your database. (optional, 4 by default)
    connections: 4,
});
```

Using [Rhai arrays](https://rhai.rs/book/language/arrays.html) and [maps](https://rhai.rs/book/language/object-maps.html#object-maps), vSL can easily fetch and update data from a mysql database.

```
#{
    connect: [
        rule "query mysql database" || {
            // Query the database.
            let records = database.query("SELECT * FROM my_table");
            
            log("info", "mysql records");
            for record in records {
                log("info", ` -> ${record}`);
            }
        }
    ]
}
```

> Check out the [greylist](../tuto/1/greylist.md) tutorial for a full example of a greylist database using mysql.