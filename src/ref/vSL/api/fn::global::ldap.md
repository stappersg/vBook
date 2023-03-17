# global::ldap


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> connect </h2>

```rust,ignore
fn connect(parameters: Map) -> Ldap
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
    id="link-connect-Note"
    class="tablinks"
    onclick="openTab(event, 'connect', 'Note')">
        Note
    </button>
    <button
    group="connect"
    id="link-connect-Example"
    class="tablinks"
    onclick="openTab(event, 'connect', 'Example')">
        Example
    </button></div>

<div group="connect" id="connect-description" style="display: block;" markdown="span" class="tabcontent">
Construct a ldap connection pool pointing to the given ldap server.


</div>

<div group="connect" id="connect-Args" class="tabcontent">

* `parameters` - A map with following parameters:
    * `url`             - A string url to connect to the database.
    * `timeout`         - Time allowed between each query to the database. (default: 30s)
    * `connections`     - Number of connections to open to the database. (default: 4)
    * `bind`            - A map of parameters to execute a simple bind operation: (optional, default: no bind)
        * `dn`          - The DN used to bind.
        * `pw`          - The password used to bind.
    * `tls`             - A map with the following parameters: (optional, default: no tls)
        * `starttls`    - `true` to use starttls when connecting to the server. (optional, default: false)
        * `cafile`      - Root certificate path to use when connecting. (optional)
                          If this parameter is not used, the client will load root certificates
                          found in the platform's native certificate store instead.
                          Be careful since loading native certificates, on some platforms,
                          involves loading and parsing a ~300KB disk file.


</div>

<div group="connect" id="connect-Return" class="tabcontent">

A service used to query the server pointed by the `url` parameter.


</div>

<div group="connect" id="connect-Error" class="tabcontent">

* The service failed to connect to the server.
* The service failed to load root certificates.


</div>

<div group="connect" id="connect-Note" class="tabcontent">

It is recommended to create a ldap service in it's own module.


</div>

<div group="connect" id="connect-Example" class="tabcontent">

```text
// Import the plugin stored in the `plugins` directory.
import "plugins/libvsmtp_plugin_ldap" as ldap;

export const directory = ldap::connect(#{
    url: "ldap://ds.example.com:1389 ",
});
```
</div>

</div>
</br>

<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> search </h2>

```rust,ignore
fn search(database: Ldap, base: String, scope: String, filter: String, attrs: Array) -> Map
```

<div class="tab">
    <button
    group="search"
    id="link-search-description"
    class="tablinks active"
    onclick="openTab(event, 'search', 'description')">
        Description
    </button>
    <button
    group="search"
    id="link-search-Args"
    class="tablinks"
    onclick="openTab(event, 'search', 'Args')">
        Args
    </button>
    <button
    group="search"
    id="link-search-Return"
    class="tablinks"
    onclick="openTab(event, 'search', 'Return')">
        Return
    </button>
    <button
    group="search"
    id="link-search-Errors"
    class="tablinks"
    onclick="openTab(event, 'search', 'Errors')">
        Errors
    </button>
    <button
    group="search"
    id="link-search-Example"
    class="tablinks"
    onclick="openTab(event, 'search', 'Example')">
        Example
    </button></div>

<div group="search" id="search-description" style="display: block;" markdown="span" class="tabcontent">
Search the ldap server for entries.


</div>

<div group="search" id="search-Args" class="tabcontent">

* `base`   - The search base, which is the starting point in the DIT for the operation.
* `scope`  - The scope, which bounds the number of entries which the operation will consider
             Can either be `base`, `one` or `sub`.
* `filter` - An expression computed for all candidate entries,
             selecting those for which it evaluates to true.
* `attrs`  - The list of attributes to retrieve from the matching entries.


</div>

<div group="search" id="search-Return" class="tabcontent">

A list of entries (as maps) containing the queried attributes for each entry.

* `result`      - Can be "ok" or "error".
* `entries`     - If `result` is set to "ok", contains an array of the following map:
    * `dn`      - The entry DN.
    * `attrs`   - The entry attributes that were searched.
* `error`       - If `result` is set to "error", contains a string with the error.


</div>

<div group="search" id="search-Errors" class="tabcontent">

* The connection timed out.
* The scope string is invalid.


</div>

<div group="search" id="search-Example" class="tabcontent">

Build a service in `services/ds.vsl`;

```text
// Import the plugin stored in the `plugins` directory.
import "plugins/libvsmtp_plugin_ldap" as ldap;

export const directory = ldap::connect(#{
    url: "ldap://ds.example.com:389 ",
    timeout: "1m",
    connections: 10,
});
```

Search the DS during filtering.

```text
import "services/ds" as srv;

#{
    rcpt: [
        rule "check recipient in DS" || {
            let address = rcpt();
            let user = recipient.local_part();

            const results = srv::directory.search(
                "ou=People,dc=example,dc=com",

                // Search the whole tree.
                "sub",

                // Match on the user id and address.
                `(|(uid=${user})(mail=${address}))`

                // Get all attributes from the entries.
                ["*"]
            );

            // ...
        }
    ],
}
</div>

</div>
</br>

<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> compare </h2>

```rust,ignore
fn compare(database: Ldap, dn: String, attr: String, val: String) -> bool
```

<div class="tab">
    <button
    group="compare"
    id="link-compare-description"
    class="tablinks active"
    onclick="openTab(event, 'compare', 'description')">
        Description
    </button>
    <button
    group="compare"
    id="link-compare-Args"
    class="tablinks"
    onclick="openTab(event, 'compare', 'Args')">
        Args
    </button>
    <button
    group="compare"
    id="link-compare-Return"
    class="tablinks"
    onclick="openTab(event, 'compare', 'Return')">
        Return
    </button>
    <button
    group="compare"
    id="link-compare-Example"
    class="tablinks"
    onclick="openTab(event, 'compare', 'Example')">
        Example
    </button></div>

<div group="compare" id="compare-description" style="display: block;" markdown="span" class="tabcontent">
Compare the value(s) of the attribute attr within an entry named by dn with the value val.


</div>

<div group="compare" id="compare-Args" class="tabcontent">

* `dn`      - name of the entry.
* `attr`    - The attribute use to compare the value.
* `val`     - expected value of the attribute.


</div>

<div group="compare" id="compare-Return" class="tabcontent">

True, if the attribute matches, false otherwise.


</div>

<div group="compare" id="compare-Example" class="tabcontent">

Build a service in `services/ds.vsl`;

```text
// Import the plugin stored in the `plugins` directory.
import "plugins/libvsmtp_plugin_ldap" as ldap;

export const directory = ldap::connect(#{
    url: "ldap://ds.example.com:389 ",
    timeout: "1m",
    connections: 10,
});
```

Compare an entry attribute during filtering.

```text
import "services/ds" as srv;

#{
    rcpt: [
        rule "check recipient in DS" || {
            let address = rcpt();
            let user = recipient.local_part();

            if srv::directory.compare(
                // Find the user in our directory.
                `uid=${user},ou=People,dc=example,dc=org`,
                // Compare the "address" attribute.
                "address",
                // Check if the given recipient address is the same as
                // the one registered in the directory.
                address.to_string(),
            ) {
                log("info", `${user} email address is registered in the directory.`);
            } else {
                log("warn", `${user}'s email address does not match the one registered in the directory.`);
            }
        }
    ],
}
</div>

</div>
</br>
