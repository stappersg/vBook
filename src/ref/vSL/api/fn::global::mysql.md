# global::mysql

This plugin exposes methods to open a pool of connexions to a mysql database using
Rhai.


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> connect </h2>

```rust,ignore
fn connect(parameters: Map) -> MySQL
```

<div class="tab">
    <button
    group="connect"
    id="link-connect-description"
    class="tablinks active"
    onclick="openTab(event, 'connect', 'description')">
        Description
    </button>
    <button
    group="connect"
    id="link-connect-Args"
    class="tablinks"
    onclick="openTab(event, 'connect', 'Args')">
        Args
    </button>
    <button
    group="connect"
    id="link-connect-Return"
    class="tablinks"
    onclick="openTab(event, 'connect', 'Return')">
        Return
    </button>
    <button
    group="connect"
    id="link-connect-Error"
    class="tablinks"
    onclick="openTab(event, 'connect', 'Error')">
        Error
    </button>
    <button
    group="connect"
    id="link-connect-Example"
    class="tablinks"
    onclick="openTab(event, 'connect', 'Example')">
        Example
    </button></div>

<div group="connect" id="connect-description" style="display: block;" markdown="span" class="tabcontent">
Open a pool of connections to a MySQL database.


</div>

<div group="connect" id="connect-Args" class="tabcontent">

* `parameters` - a map of the following parameters:
    * `url` - a string url to connect to the database.
    * `timeout` - time allowed between each query to the database. (default: 30s)
    * `connections` - Number of connections to open to the database. (default: 4)


</div>

<div group="connect" id="connect-Return" class="tabcontent">

A service used to query the database pointed by the `url` parameter.


</div>

<div group="connect" id="connect-Error" class="tabcontent">

* The service failed to connect to the database.


</div>

<div group="connect" id="connect-Example" class="tabcontent">

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
</div>

</div>
</br>

<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> query </h2>

```rust,ignore
fn query(database: MySQL, query: SharedObject) -> Array
fn query(database: MySQL, query: String) -> Array
```

<div class="tab">
    <button
    group="query"
    id="link-query-description"
    class="tablinks active"
    onclick="openTab(event, 'query', 'description')">
        Description
    </button>
    <button
    group="query"
    id="link-query-Args"
    class="tablinks"
    onclick="openTab(event, 'query', 'Args')">
        Args
    </button>
    <button
    group="query"
    id="link-query-Return"
    class="tablinks"
    onclick="openTab(event, 'query', 'Return')">
        Return
    </button>
    <button
    group="query"
    id="link-query-Example"
    class="tablinks"
    onclick="openTab(event, 'query', 'Example')">
        Example
    </button></div>

<div group="query" id="query-description" style="display: block;" markdown="span" class="tabcontent">
Query the database.


</div>

<div group="query" id="query-Args" class="tabcontent">

* `query` - The query to execute.


</div>

<div group="query" id="query-Return" class="tabcontent">

A list of records.


</div>

<div group="query" id="query-Example" class="tabcontent">

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
</div>

</div>
</br>
