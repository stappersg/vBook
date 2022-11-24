# CSV

The csv plugin lets you open, read and write csv databases.

## Install

Install `libvsmtp_plugin_csv.so` in `/usr/lib/vsmtp`, then use a symbolic link in your configuration.

```sh
ln -s /usr/lib/vsmtp/libvsmtp_plugin_csv.so /etc/vsmtp/plugins/libvsmtp_plugin_csv.so
```

## Using the plugin

```js
import "plugins/libvsmtp_plugin_csv" as db;

export const database = db::csv(#{
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
    //          time it is queried. Use it only if you have a small database.
    refresh: "always",
    // The delimiter character used in the csv file.
    delimiter: ",",
});

// query & update the database.
let john = greylist.get("john");
greylist.set(["new", "user", "new.user@example.com"]);
greylist.rm("green");

// manipulating a record.

// ["john", "doe", "john.doe@example.com"]
print(john);

// records are stored in vsl arrays.
// to get a field in a record, simply use it's index.

// "john.doe@example.com"
print(john[2]);
```