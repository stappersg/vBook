# global::mysql

This plugin exposes methods to open a pool of connexions to a mysql database using
Rhai.


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> connect </h2>

```rust,ignore
fn connect(parameters: Map) -> MySQL
```

<details>
<summary markdown="span"> details </summary>

Open a pool of connections to a MySQL database.

# Args

* `parameters` - a map of the following parameters:
    * `url` - a string url to connect to the database.
    * `timeout` - time allowed between each query to the database. (default: 30s)
    * `connections` - Number of connections to open to the database. (default: 4)

# Return

A service used to query the database pointed by the `url` parameter.

# Error

* The service failed to connect to the database.

# Example

```text
// Import the plugin stored in the `plugins` directory.
import "plugins/libvsmtp_plugin_mysql" as mysql;

export const database = mysql::connect(#{
    // Connect to a database on the system with the 'greylist-manager' user and 'my-password' password.
    url: "mysql://localhost/?user=greylist-manager&password=my-password",
    timeout: "1m",
    connections: 1,
});
```
</details>

</div>
</br>

<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> query </h2>

```rust,ignore
fn query(database: MySQL, query: String) -> Array
fn query(database: MySQL, query: SharedObject) -> Array
```

<details>
<summary markdown="span"> details </summary>

Query the database.

# Args

* `query` - The query to execute.

# Return

A list of records.

# Example

Build a service in `services/database.vsl`;

```text
// Import the plugin stored in the `plugins` directory.
import "plugins/libvsmtp_plugin_mysql" as mysql;

export const database = mysql::connect(#{
    // Connect to a database on the system with the 'greylist-manager' user and 'my-password' password.
    url: "mysql://localhost/?user=greylist-manager&password=my-password",
    timeout: "1m",
    connections: 1,
});
```

Query the database during filtering.

```text
import "services/database" as srv;

#{
    connect: [
        action "get records from my database" || {
            // For the sake of this example, we assume that there is a populated
            // table called 'my_table' in the database.
            const records = srv::database.query("SELECT * FROM my_table");

            // `records` is an array, we can run a for loop and print all records.
            log("info", "fetching mysql records ...");
            for record in records {
                log("info", ` -> ${record}`);
            }
        }
    ],
}
```
</details>

</div>
</br>
