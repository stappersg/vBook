# global::memcached

This plugin exposes methods to open a pool of connexions to a memached server using
Rhai.


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> connect </h2>

```rust,ignore
fn connect(parameters: Map) -> Cache
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
Open a pool of connections to a Memcached server.


</div>

<div group="connect" id="connect-Args" class="tabcontent">

* `parameters` - a map of the following parameters:
    * `url` - a string url to connect to the server.
    * `timeout` - time allowed between each interaction with the server. (default: 30s)
    * `connections` - Number of connections to open to the server. (default: 4)


</div>

<div group="connect" id="connect-Return" class="tabcontent">

A service used to access the memcached server pointed by the `url` parameter.


</div>

<div group="connect" id="connect-Error" class="tabcontent">

* The service failed to connect to the server.


</div>

<div group="connect" id="connect-Example" class="tabcontent">

```text
// Import the plugin stored in the `plugins` directory.
import "plugins/libvsmtp_plugin_memcached" as cache;

export const cache = cache::connect(#{
    // Connect to a server on the port 11211 with a timeout.
    url: "memcache://localhost:11211",
    timeout: "10s",
    connections: 1,
});
```
</div>

</div>
</br>

<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> flush </h2>

```rust,ignore
fn flush(cache: Cache) -> ()
```

<div class="tab">
    <button
    group="flush"
    id="link-flush-description"
    class="tablinks active"
    onclick="openTab(event, 'flush', 'description')">
        Description
    </button>
    <button
    group="flush"
    id="link-flush-Example"
    class="tablinks"
    onclick="openTab(event, 'flush', 'Example')">
        Example
    </button></div>

<div group="flush" id="flush-description" style="display: block;" markdown="span" class="tabcontent">
Flush all cache on the server immediately


</div>

<div group="flush" id="flush-Example" class="tabcontent">

Build a service in `services/cache.vsl`;

```text
// Import the plugin stored in the `plugins` directory.
import "plugins/libvsmtp_plugin_memcached" as cache;

export const srv = cache::connect(#{
    url: "memcache://localhost:11211",
    timeout: "10s",
    connections: 1,
});
```

Flush all cache during filtering.

```text
import "services/cache" as srv;

#{
    connect: [
        action "flush the cache" || {
            srv::cache.flush();
        }
    ],
}
```
</div>

</div>
</br>

<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> get </h2>

```rust,ignore
fn get(cache: Cache, key: String) -> ?
```

<div class="tab">
    <button
    group="get"
    id="link-get-description"
    class="tablinks active"
    onclick="openTab(event, 'get', 'description')">
        Description
    </button>
    <button
    group="get"
    id="link-get-Args"
    class="tablinks"
    onclick="openTab(event, 'get', 'Args')">
        Args
    </button>
    <button
    group="get"
    id="link-get-Return"
    class="tablinks"
    onclick="openTab(event, 'get', 'Return')">
        Return
    </button>
    <button
    group="get"
    id="link-get-Example"
    class="tablinks"
    onclick="openTab(event, 'get', 'Example')">
        Example
    </button></div>

<div group="get" id="get-description" style="display: block;" markdown="span" class="tabcontent">
Get something from the server.


</div>

<div group="get" id="get-Args" class="tabcontent">

* `key` - The key you want to get the value from


</div>

<div group="get" id="get-Return" class="tabcontent">

A rhai::Dynamic with the value inside


</div>

<div group="get" id="get-Example" class="tabcontent">

Build a service in `services/cache.vsl`;

```text
// Import the plugin stored in the `plugins` directory.
import "plugins/libvsmtp_plugin_memcached" as cache;

export const srv = cache::connect(#{
    url: "memcache://localhost:11211",
    timeout: "10s",
    connections: 1,
});
```

Get the value wanted during filtering.

```text
import "services/cache" as srv;

#{
    connect: [
        action "get value from my memcached server" || {
            // For the sake of this example, we assume that there is a "client_ip" as a key and "0.0.0.0" as its value.
            const client_ip = srv::cache.get("client_ip");
            log("info", `ip of my client is: ${client_ip}`);
        }
    ],
}
```
</div>

</div>
</br>

<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> get_with_cas </h2>

```rust,ignore
fn get_with_cas(cache: Cache, key: String) -> ?
```

<div class="tab">
    <button
    group="get_with_cas"
    id="link-get_with_cas-description"
    class="tablinks active"
    onclick="openTab(event, 'get_with_cas', 'description')">
        Description
    </button>
    <button
    group="get_with_cas"
    id="link-get_with_cas-Args"
    class="tablinks"
    onclick="openTab(event, 'get_with_cas', 'Args')">
        Args
    </button>
    <button
    group="get_with_cas"
    id="link-get_with_cas-Return"
    class="tablinks"
    onclick="openTab(event, 'get_with_cas', 'Return')">
        Return
    </button>
    <button
    group="get_with_cas"
    id="link-get_with_cas-Example"
    class="tablinks"
    onclick="openTab(event, 'get_with_cas', 'Example')">
        Example
    </button></div>

<div group="get_with_cas" id="get_with_cas-description" style="display: block;" markdown="span" class="tabcontent">
Get a value from the server with its cas_id and its expiration seconds.


</div>

<div group="get_with_cas" id="get_with_cas-Args" class="tabcontent">

* `key` - The key you want to get the value from


</div>

<div group="get_with_cas" id="get_with_cas-Return" class="tabcontent">

A rhai::Dynamic with the values inside. Keys are "value", "expiration", "cas_id". If the key doesn't exist, returns 0


</div>

<div group="get_with_cas" id="get_with_cas-Example" class="tabcontent">

Build a service in `services/cache.vsl`;

```text
// Import the plugin stored in the `plugins` directory.
import "plugins/libvsmtp_plugin_memcached" as cache;

export const srv = cache::connect(#{
    url: "memcache://localhost:11211",
    timeout: "10s",
    connections: 1,
});
```

Get the value wanted during filtering.

```text
import "services/cache" as srv;

#{
    connect: [
        action "get value from my memcached server" || {
            // For the sake of this example, we assume that there is a "client_ip" as a key and "0.0.0.0" as its value.
            const cas_id = srv::cache.get_with_cas("client_ip").cas_id;
            log("info", `id is: ${cas_id}`);
        }
    ],
}
```
</div>

</div>
</br>

<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> gets </h2>

```rust,ignore
fn gets(cache: Cache, keys: Array) -> ?
```

<div class="tab">
    <button
    group="gets"
    id="link-gets-description"
    class="tablinks active"
    onclick="openTab(event, 'gets', 'description')">
        Description
    </button>
    <button
    group="gets"
    id="link-gets-Args"
    class="tablinks"
    onclick="openTab(event, 'gets', 'Args')">
        Args
    </button>
    <button
    group="gets"
    id="link-gets-Return"
    class="tablinks"
    onclick="openTab(event, 'gets', 'Return')">
        Return
    </button>
    <button
    group="gets"
    id="link-gets-Example"
    class="tablinks"
    onclick="openTab(event, 'gets', 'Example')">
        Example
    </button></div>

<div group="gets" id="gets-description" style="display: block;" markdown="span" class="tabcontent">
Gets multiple value from mutliple key from the server.


</div>

<div group="gets" id="gets-Args" class="tabcontent">

* `keys` - The keys you want to get the values from


</div>

<div group="gets" id="gets-Return" class="tabcontent">

A rhai::Map<String, rhai::Dynamic> with the values inside


</div>

<div group="gets" id="gets-Example" class="tabcontent">

Build a service in `services/cache.vsl`;

```text
// Import the plugin stored in the `plugins` directory.
import "plugins/libvsmtp_plugin_memcached" as cache;

export const srv = cache::connect(#{
    url: "memcache://localhost:11211",
    timeout: "10s",
    connections: 1,
});
```

Gets all the values wanted during filtering.

```text
import "services/cache" as srv;

#{
    connect: [
        action "get value from my memcached server" || {
            // For the sake of this example, we assume that there is a server filled with multiple values
            const client_ips = srv::cache.gets(["client1_ip", "client2_ip", "client3_ip"]);
            log("info", `client 1: ${client_ips["client1_ip"]}`);
            log("info", `client 2: ${client_ips["client2_ip"]}`);
            log("info", `client 3: ${client_ips["client3_ip"]}`);
        }
    ],
}
```
</div>

</div>
</br>

<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> gets_with_cas </h2>

```rust,ignore
fn gets_with_cas(cache: Cache, keys: Array) -> ?
```

<div class="tab">
    <button
    group="gets_with_cas"
    id="link-gets_with_cas-description"
    class="tablinks active"
    onclick="openTab(event, 'gets_with_cas', 'description')">
        Description
    </button>
    <button
    group="gets_with_cas"
    id="link-gets_with_cas-Args"
    class="tablinks"
    onclick="openTab(event, 'gets_with_cas', 'Args')">
        Args
    </button>
    <button
    group="gets_with_cas"
    id="link-gets_with_cas-Return"
    class="tablinks"
    onclick="openTab(event, 'gets_with_cas', 'Return')">
        Return
    </button>
    <button
    group="gets_with_cas"
    id="link-gets_with_cas-Example"
    class="tablinks"
    onclick="openTab(event, 'gets_with_cas', 'Example')">
        Example
    </button></div>

<div group="gets_with_cas" id="gets_with_cas-description" style="display: block;" markdown="span" class="tabcontent">
Gets multiple value from mutliple key from the server with their cas_id, expiration seconds, key and value.


</div>

<div group="gets_with_cas" id="gets_with_cas-Args" class="tabcontent">

* `keys` - The keys you want to get the values from


</div>

<div group="gets_with_cas" id="gets_with_cas-Return" class="tabcontent">

A rhai::Array<rhai::Map> with the values cas_id, expiration, key and value inside


</div>

<div group="gets_with_cas" id="gets_with_cas-Example" class="tabcontent">

Build a service in `services/cache.vsl`;

```text
// Import the plugin stored in the `plugins` directory.
import "plugins/libvsmtp_plugin_memcached" as cache;

export const srv = cache::connect(#{
    url: "memcache://localhost:11211",
    timeout: "10s",
    connections: 1,
});
```

Gets all the values wanted during filtering.

```text
import "services/cache" as srv;

#{
    connect: [
        action "get value from my memcached server" || {
            // For the sake of this example, we assume that there is a server filled with multiple values
            const entries = srv::memcached.gets_with_cas(["client1_ip", "client2_ip", "client3_ip"]);
            const cas_id = entries.find(|v| v.key == "client1_ip").cas_id;
            log("info", `id is: ${cas_id}`);
        }
    ],
}
```
</div>

</div>
</br>

<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> set </h2>

```rust,ignore
fn set(cache: Cache, key: String, value: ?, duration: int) -> ()
```

<div class="tab">
    <button
    group="set"
    id="link-set-description"
    class="tablinks active"
    onclick="openTab(event, 'set', 'description')">
        Description
    </button>
    <button
    group="set"
    id="link-set-Args"
    class="tablinks"
    onclick="openTab(event, 'set', 'Args')">
        Args
    </button>
    <button
    group="set"
    id="link-set-Example"
    class="tablinks"
    onclick="openTab(event, 'set', 'Example')">
        Example
    </button></div>

<div group="set" id="set-description" style="display: block;" markdown="span" class="tabcontent">
Set a value with its associate key into the server with expiration seconds.


</div>

<div group="set" id="set-Args" class="tabcontent">

* `key` - The key you want to allocate with the value
* `value` - The value you want to store
* `duration` - The duration time you want the value to remain in cache


</div>

<div group="set" id="set-Example" class="tabcontent">

Build a service in `services/cache.vsl`;

```text
// Import the plugin stored in the `plugins` directory.
import "plugins/libvsmtp_plugin_memcached" as cache;

export const srv = cache::connect(#{
    url: "memcache://localhost:11211",
    timeout: "10s",
    connections: 1,
});
```

Set a value during filtering.

```text
import "services/cache" as srv;

#{
    connect: [
        action "set value into my memcached server" || {
            srv::cache.set("client_ip", "0.0.0.0", 0);
            const client_ip = srv::cache.get("client_ip");
            log("info", `ip of my client is: ${client_ip}`);
        }
    ],
}
```
</div>

</div>
</br>

<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> cas </h2>

```rust,ignore
fn cas(cache: Cache, key: String, value: ?, expiration: int, cas_id: int) -> bool
```

<div class="tab">
    <button
    group="cas"
    id="link-cas-description"
    class="tablinks active"
    onclick="openTab(event, 'cas', 'description')">
        Description
    </button>
    <button
    group="cas"
    id="link-cas-Args"
    class="tablinks"
    onclick="openTab(event, 'cas', 'Args')">
        Args
    </button>
    <button
    group="cas"
    id="link-cas-Example"
    class="tablinks"
    onclick="openTab(event, 'cas', 'Example')">
        Example
    </button></div>

<div group="cas" id="cas-description" style="display: block;" markdown="span" class="tabcontent">
Compare and swap a key with the associate value into memcached server with expiration seconds.


</div>

<div group="cas" id="cas-Args" class="tabcontent">

* `key` - The key you want to swap
* `value` - The value you want to store
* `expiration` - The duration time you want the value to remain in cache
* `cas_id` - The id which is obtained from a previous call to gets


</div>

<div group="cas" id="cas-Example" class="tabcontent">

Build a service in `services/cache.vsl`;

```text
// Import the plugin stored in the `plugins` directory.
import "plugins/libvsmtp_plugin_memcached" as cache;

export const srv = cache::connect(#{
    url: "memcache://localhost:11211",
    timeout: "10s",
    connections: 1,
});
```

Compare and swap a value during filtering

```text
import "services/cache" as srv;

#{
    connect: [
        action "cas a key in the server" || {
            srv::cache.set("foo", "bar", 0);
            let result = srv::cache.get_with_cas("foo");
            srv::cache.cas("foo", "bar2", 0, result.cas_id);
        }
    ],
}
```
</div>

</div>
</br>

<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> add </h2>

```rust,ignore
fn add(cache: Cache, key: String, value: ?, duration: int) -> ()
```

<div class="tab">
    <button
    group="add"
    id="link-add-description"
    class="tablinks active"
    onclick="openTab(event, 'add', 'description')">
        Description
    </button>
    <button
    group="add"
    id="link-add-Args"
    class="tablinks"
    onclick="openTab(event, 'add', 'Args')">
        Args
    </button>
    <button
    group="add"
    id="link-add-Example"
    class="tablinks"
    onclick="openTab(event, 'add', 'Example')">
        Example
    </button></div>

<div group="add" id="add-description" style="display: block;" markdown="span" class="tabcontent">
Add a key with associate value into memcached server with expiration seconds.


</div>

<div group="add" id="add-Args" class="tabcontent">

* `key` - The key you want to allocate with the value
* `value` - The value you want to store
* `duration` - The duration time you want the value to remain in cache


</div>

<div group="add" id="add-Example" class="tabcontent">

Build a service in `services/cache.vsl`;

```text
// Import the plugin stored in the `plugins` directory.
import "plugins/libvsmtp_plugin_memcached" as cache;

export const srv = cache::connect(#{
    url: "memcache://localhost:11211",
    timeout: "10s",
    connections: 1,
});
```

Add a value during filtering.

```text
import "services/cache" as srv;

#{
    connect: [
        action "add value into my memcached server" || {
            // Will get an error if the key already exists
            srv::cache.add("client_ip", "0.0.0.0", 0);
            const client_ip = srv::cache.get("client_ip");
            log("info", `ip of my client is: ${client_ip}`);
        }
    ],
}
```
</div>

</div>
</br>

<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> replace </h2>

```rust,ignore
fn replace(cache: Cache, key: String, value: ?, duration: int) -> ()
```

<div class="tab">
    <button
    group="replace"
    id="link-replace-description"
    class="tablinks active"
    onclick="openTab(event, 'replace', 'description')">
        Description
    </button>
    <button
    group="replace"
    id="link-replace-Args"
    class="tablinks"
    onclick="openTab(event, 'replace', 'Args')">
        Args
    </button>
    <button
    group="replace"
    id="link-replace-Example"
    class="tablinks"
    onclick="openTab(event, 'replace', 'Example')">
        Example
    </button></div>

<div group="replace" id="replace-description" style="display: block;" markdown="span" class="tabcontent">
Replace a key with associate value into memcached server with expiration seconds.


</div>

<div group="replace" id="replace-Args" class="tabcontent">

* `key` - The key you want to replace with the value
* `value` - The value you want to store
* `duration` - The duration time you want the value to remain in cache


</div>

<div group="replace" id="replace-Example" class="tabcontent">

Build a service in `services/cache.vsl`;

```text
// Import the plugin stored in the `plugins` directory.
import "plugins/libvsmtp_plugin_memcached" as cache;

export const srv = cache::connect(#{
    url: "memcache://localhost:11211",
    timeout: "10s",
    connections: 1,
});
```

Replace a value during filtering.

```text
import "services/cache" as srv;

#{
    connect: [
        action "replace value into my memcached server" || {
            srv::cache.set("client_ip", "0.0.0.0", 0);
            // Will get an error if the key doesn't exist
            srv::cache.replace("client_ip", "255.255.255.255", 0);
            const client_ip = srv::cache.get("client_ip");
            log("info", `ip of my client is: ${client_ip}`);
        }
    ],
}
```
</div>

</div>
</br>

<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> append </h2>

```rust,ignore
fn append(cache: Cache, key: String, value: ?) -> ()
```

<div class="tab">
    <button
    group="append"
    id="link-append-description"
    class="tablinks active"
    onclick="openTab(event, 'append', 'description')">
        Description
    </button>
    <button
    group="append"
    id="link-append-Args"
    class="tablinks"
    onclick="openTab(event, 'append', 'Args')">
        Args
    </button>
    <button
    group="append"
    id="link-append-Example"
    class="tablinks"
    onclick="openTab(event, 'append', 'Example')">
        Example
    </button></div>

<div group="append" id="append-description" style="display: block;" markdown="span" class="tabcontent">
Append value to the key.


</div>

<div group="append" id="append-Args" class="tabcontent">

* `key` - The key you want to append with the value
* `value` - The value you want to append


</div>

<div group="append" id="append-Example" class="tabcontent">

Build a service in `services/cache.vsl`;

```text
// Import the plugin stored in the `plugins` directory.
import "plugins/libvsmtp_plugin_memcached" as cache;

export const srv = cache::connect(#{
    url: "memcache://localhost:11211",
    timeout: "10s",
    connections: 1,
});
```

Append a value during filtering.

```text
import "services/cache" as srv;

#{
    connect: [
        action "append value into my memcached server" || {
            srv::cache.set("client_ip", "0.0.", 0);
            // Will get an error if the key doesn't exist
            srv::cache.append("client_ip", "0.0");
            const client_ip = srv::cache.get("client_ip");
            log("info", `ip of my client is: ${client_ip}`);
        }
    ],
}
```
</div>

</div>
</br>

<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> prepend </h2>

```rust,ignore
fn prepend(cache: Cache, key: String, value: ?) -> ()
```

<div class="tab">
    <button
    group="prepend"
    id="link-prepend-description"
    class="tablinks active"
    onclick="openTab(event, 'prepend', 'description')">
        Description
    </button>
    <button
    group="prepend"
    id="link-prepend-Args"
    class="tablinks"
    onclick="openTab(event, 'prepend', 'Args')">
        Args
    </button>
    <button
    group="prepend"
    id="link-prepend-Example"
    class="tablinks"
    onclick="openTab(event, 'prepend', 'Example')">
        Example
    </button></div>

<div group="prepend" id="prepend-description" style="display: block;" markdown="span" class="tabcontent">
Prepend value to the key.


</div>

<div group="prepend" id="prepend-Args" class="tabcontent">

* `key` - The key you want to prepend with the value
* `value` - The value you want to prepend


</div>

<div group="prepend" id="prepend-Example" class="tabcontent">

Build a service in `services/cache.vsl`;

```text
// Import the plugin stored in the `plugins` directory.
import "plugins/libvsmtp_plugin_memcached" as cache;

export const srv = cache::connect(#{
    url: "memcache://localhost:11211",
    timeout: "10s",
    connections: 1,
});
```

Prepend a value during filtering.

```text
import "services/cache" as srv;

#{
    connect: [
        action "prepend value into my memcached server" || {
            srv::cache.set("client_ip", ".0.0", 0);
            // Will get an error if the key doesn't exist
            srv::cache.prepend("client_ip", "0.0");
            const client_ip = srv::cache.get("client_ip");
            log("info", `ip of my client is: ${client_ip}`);
        }
    ],
}
```
</div>

</div>
</br>

<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> delete </h2>

```rust,ignore
fn delete(cache: Cache, key: String) -> bool
```

<div class="tab">
    <button
    group="delete"
    id="link-delete-description"
    class="tablinks active"
    onclick="openTab(event, 'delete', 'description')">
        Description
    </button>
    <button
    group="delete"
    id="link-delete-Args"
    class="tablinks"
    onclick="openTab(event, 'delete', 'Args')">
        Args
    </button>
    <button
    group="delete"
    id="link-delete-Example"
    class="tablinks"
    onclick="openTab(event, 'delete', 'Example')">
        Example
    </button></div>

<div group="delete" id="delete-description" style="display: block;" markdown="span" class="tabcontent">
Delete value of the specified key.


</div>

<div group="delete" id="delete-Args" class="tabcontent">

* `key` - The key you want the value to be deleted


</div>

<div group="delete" id="delete-Example" class="tabcontent">

Build a service in `services/cache.vsl`;

```text
// Import the plugin stored in the `plugins` directory.
import "plugins/libvsmtp_plugin_memcached" as cache;

export const srv = cache::connect(#{
    url: "memcache://localhost:11211",
    timeout: "10s",
    connections: 1,
});
```

Delete a value during filtering.

```text
import "services/cache" as srv;

#{
    connect: [
        action "delete value into my memcached server" || {
            srv::cache.set("client_ip", "0.0.0.0", 0);
            srv::cache.delete("client_ip");
            // Will return nothing
            const client_ip = srv::cache.get("client_ip");
            log("info", `ip of my client is: ${client_ip}`);
        }
    ],
}
```
</div>

</div>
</br>

<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> increment </h2>

```rust,ignore
fn increment(cache: Cache, key: String, value: int) -> ()
```

<div class="tab">
    <button
    group="increment"
    id="link-increment-description"
    class="tablinks active"
    onclick="openTab(event, 'increment', 'description')">
        Description
    </button>
    <button
    group="increment"
    id="link-increment-Args"
    class="tablinks"
    onclick="openTab(event, 'increment', 'Args')">
        Args
    </button>
    <button
    group="increment"
    id="link-increment-Example"
    class="tablinks"
    onclick="openTab(event, 'increment', 'Example')">
        Example
    </button></div>

<div group="increment" id="increment-description" style="display: block;" markdown="span" class="tabcontent">
Increment value of the specified key.


</div>

<div group="increment" id="increment-Args" class="tabcontent">

* `key` - The key you want the value to be incremented
* `value` - Amount of the increment


</div>

<div group="increment" id="increment-Example" class="tabcontent">

Build a service in `services/cache.vsl`;

```text
// Import the plugin stored in the `plugins` directory.
import "plugins/libvsmtp_plugin_memcached" as cache;

export const srv = cache::connect(#{
    url: "memcache://localhost:11211",
    timeout: "10s",
    connections: 1,
});
```

Increment a value during filtering.

```text
import "services/cache" as srv;

#{
    connect: [
        action "increment value into my memcached server" || {
            srv::cache.set("nb_of_client", 1, 0);
            srv::cache.increment("nb_of_client", 21);
            const nb_of_client = srv::cache.get("nb_of_client");
            log("info", `nb of client is: ${nb_of_client}`);
        }
    ],
}
```
</div>

</div>
</br>

<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> decrement </h2>

```rust,ignore
fn decrement(cache: Cache, key: String, value: int) -> ()
```

<div class="tab">
    <button
    group="decrement"
    id="link-decrement-description"
    class="tablinks active"
    onclick="openTab(event, 'decrement', 'description')">
        Description
    </button>
    <button
    group="decrement"
    id="link-decrement-Args"
    class="tablinks"
    onclick="openTab(event, 'decrement', 'Args')">
        Args
    </button>
    <button
    group="decrement"
    id="link-decrement-Example"
    class="tablinks"
    onclick="openTab(event, 'decrement', 'Example')">
        Example
    </button></div>

<div group="decrement" id="decrement-description" style="display: block;" markdown="span" class="tabcontent">
Decrement value of the specified key.


</div>

<div group="decrement" id="decrement-Args" class="tabcontent">

* `key` - The key you want the value to be decremented
* `value` - Amount of the Decrement


</div>

<div group="decrement" id="decrement-Example" class="tabcontent">

Build a service in `services/cache.vsl`;

```text
// Import the plugin stored in the `plugins` directory.
import "plugins/libvsmtp_plugin_memcached" as cache;

export const srv = cache::connect(#{
    url: "memcache://localhost:11211",
    timeout: "10s",
    connections: 1,
});
```

Decrement a value during filtering.

```text
import "services/cache" as srv;

#{
    connect: [
        action "decrement value into my memcached server" || {
            srv::cache.set("nb_of_client", 21, 0);
            srv::cache.decrement("nb_of_client", 1);
            const nb_of_client = srv::cache.get("nb_of_client");
            log("info", `nb of client is: ${nb_of_client}`);
        }
    ],
}
```
</div>

</div>
</br>

<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> touch </h2>

```rust,ignore
fn touch(cache: Cache, key: String, duration: int) -> ()
```

<div class="tab">
    <button
    group="touch"
    id="link-touch-description"
    class="tablinks active"
    onclick="openTab(event, 'touch', 'description')">
        Description
    </button>
    <button
    group="touch"
    id="link-touch-Args"
    class="tablinks"
    onclick="openTab(event, 'touch', 'Args')">
        Args
    </button>
    <button
    group="touch"
    id="link-touch-Example"
    class="tablinks"
    onclick="openTab(event, 'touch', 'Example')">
        Example
    </button></div>

<div group="touch" id="touch-description" style="display: block;" markdown="span" class="tabcontent">
Set a new expiration time for a exist key.


</div>

<div group="touch" id="touch-Args" class="tabcontent">

* `key` - The key you want to change the expiration time
* `duration` - Amount of expiration time


</div>

<div group="touch" id="touch-Example" class="tabcontent">

Build a service in `services/cache.vsl`;

```text
// Import the plugin stored in the `plugins` directory.
import "plugins/libvsmtp_plugin_memcached" as cache;

export const srv = cache::connect(#{
    url: "memcache://localhost:11211",
    timeout: "10s",
    connections: 1,
});
```

Change an expiration time during filtering.

```text
import "services/cache" as srv;

#{
    connect: [
        action "change expiration time of a value into my memcached server" || {
            srv::cache.set("nb_of_client", 21, 5000);
            srv::cache.touch("nb_of_client", 0);
            const nb_of_client = srv::cache.get("nb_of_client");
            log("info", `nb of client is: ${nb_of_client}`);
        }
    ],
}
```
</div>

</div>
</br>

<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> stats </h2>

```rust,ignore
fn stats(cache: Cache) -> String
```

<div class="tab">
    <button
    group="stats"
    id="link-stats-description"
    class="tablinks active"
    onclick="openTab(event, 'stats', 'description')">
        Description
    </button>
    <button
    group="stats"
    id="link-stats-Return"
    class="tablinks"
    onclick="openTab(event, 'stats', 'Return')">
        Return
    </button>
    <button
    group="stats"
    id="link-stats-Example"
    class="tablinks"
    onclick="openTab(event, 'stats', 'Example')">
        Example
    </button></div>

<div group="stats" id="stats-description" style="display: block;" markdown="span" class="tabcontent">
Only for debugging purposes, get all server's statistics in a formatted string


</div>

<div group="stats" id="stats-Return" class="tabcontent">

A formatted string


</div>

<div group="stats" id="stats-Example" class="tabcontent">

Build a service in `services/cache.vsl`;

```text
// Import the plugin stored in the `plugins` directory.
import "plugins/libvsmtp_plugin_memcached" as cache;

export const srv = cache::connect(#{
    url: "memcache://localhost:11211",
    timeout: "10s",
    connections: 1,
});
```

Display the server statistics during filtering.

```text
import "services/cache" as srv;

#{
    connect: [
        action "show statistics of my memcached server" || {
            const stats = srv::cache.stats();
            log("info", stats);
        }
    ],
}
```
</div>

</div>
</br>
