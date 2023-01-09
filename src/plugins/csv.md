# CSV

The csv plugin can open, read and write to csv databases.

## Install

Install `libvsmtp_plugin_csv.so` in `/usr/lib/vsmtp`, then use a symbolic link in the configuration.

```sh
ln -s /usr/lib/vsmtp/libvsmtp_plugin_csv.so /etc/vsmtp/plugins/libvsmtp_plugin_csv.so
```

## Using the plugin

```rust,ignore
import "plugins/libvsmtp_plugin_csv" as db;

export const user_accounts = db::csv(#{
    // The path to the csv database.
    connector: "/db/user_accounts.csv",
    // The access mode of the database. Can be:
    // `O_RDONLY`, `O_WRONLY` or `O_RDWR`.
    access: "O_RDONLY",
    // The refresh mode of the database.
    // Can be "always" (database is always refreshed once queried)
    // or "no" (database is readonly and never refreshed).
    //
    // WARNING: using the "always" option can make vsmtp really slow,
    //          because it has to pull the whole database in memory every
    //          time it is queried. Use it only with a small database.
    refresh: "always",
    // The delimiter character used in the csv file.
    delimiter: ",",
});
```

Here is a rule using the csv service.

```
import "services/databases" as db;

#{
    mail: [
        rule "is sender in database ?" || {
            // query the database.
            // Let's assume that the `ctx::mail_from()` value is `john.doe@example.com`.
            // `db::user_accounts.get` return an array representing the selected row with
            // the key passed as parameter.
            let user = db::user_accounts.get(ctx::mail_from().local_part);

            // The record returned is an array `["john.doe", "john.doe@example.com"]`.
            if user != [] {
                // We can select columns by index.
                log("info", `A trusted client just connected: user=${user[0]}, email=${user[1]}`)
            }

            state::next()
        }
    ]
}
```