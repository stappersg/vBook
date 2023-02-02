# global::memcached

This plugin exposes methods to open a pool of connexions to a memached server using
Rhai.


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> add </h2>

```rust,ignore
fn add(cache: Cache, key: String, value: ?, duration: int) -> ()
```

<details>
<summary markdown="span"> details </summary>

Add a key with associate value into memcached server with expiration seconds.

# Args

* `key` - The key you want to allocate with the value
* `value` - The value you want to store
* `duration` - The duration time you want the value to remain in cache

# Example

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
            srv.add("client_ip", "0.0.0.0", 0);
            const client_ip = srv.get("client_ip");
            log("info", `ip of my client is: ${client_ip}`);
        }
    ],
}
```
</details>

</div>
</br>

<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> append </h2>

```rust,ignore
fn append(cache: Cache, key: String, value: ?) -> ()
```

<details>
<summary markdown="span"> details </summary>

Append value to the key.

# Args

* `key` - The key you want to append with the value
* `value` - The value you want to append

# Example

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
            srv.set("client_ip", "0.0.", 0);
            // Will get an error if the key doesn't exist
            srv.append("client_ip", "0.0");
            const client_ip = srv.get("client_ip");
            log("info", `ip of my client is: ${client_ip}`);
        }
    ],
}
```
</details>

</div>
</br>

<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> cas </h2>

```rust,ignore
fn cas(cache: Cache, key: String, value: ?, expiration: int, cas_id: int) -> bool
```

<details>
<summary markdown="span"> details </summary>

Compare and swap a key with the associate value into memcached server with expiration seconds.

# Args

* `key` - The key you want to swap
* `value` - The value you want to store
* `expiration` - The duration time you want the value to remain in cache
* `cas_id` - The id which is obtained from a previous call to gets

# Example

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
            srv.set("foo", "bar", 0);
            let result = srv.get_with_cas("foo");
            srv.cas("foo", "bar2", 0, result.cas_id);
        }
    ],
}
```
</details>

</div>
</br>

<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> connect </h2>

```rust,ignore
fn connect(parameters: Map) -> Cache
```

<details>
<summary markdown="span"> details </summary>

Open a pool of connections to a Memcached server.

# Args

* `parameters` - a map of the following parameters:
    * `url` - a string url to connect to the server.
    * `timeout` - time allowed between each interaction with the server. (default: 30s)
    * `connections` - Number of connections to open to the server. (default: 4)

# Return

A service used to access the memcached server pointed by the `url` parameter.

# Error

* The service failed to connect to the server.

# Example

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
</details>

</div>
</br>

<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> decrement </h2>

```rust,ignore
fn decrement(cache: Cache, key: String, value: int) -> ()
```

<details>
<summary markdown="span"> details </summary>

Decrement value of the specified key.

# Args

* `key` - The key you want the value to be decremented
* `value` - Amount of the Decrement

# Example

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
            srv.set("nb_of_client", 21, 0);
            srv.decrement("nb_of_client", 1);
            const nb_of_client = srv.get("nb_of_client");
            log("info", `nb of client is: ${nb_of_client}`);
        }
    ],
}
```
</details>

</div>
</br>

<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> delete </h2>

```rust,ignore
fn delete(cache: Cache, key: String) -> bool
```

<details>
<summary markdown="span"> details </summary>

Delete value of the specified key.

# Args

* `key` - The key you want the value to be deleted

# Example

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
            srv.set("client_ip", "0.0.0.0", 0);
            srv.delete("client_ip");
            // Will return nothing
            const client_ip = srv.get("client_ip");
            log("info", `ip of my client is: ${client_ip}`);
        }
    ],
}
```
</details>

</div>
</br>

<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> flush </h2>

```rust,ignore
fn flush(cache: Cache) -> ()
```

<details>
<summary markdown="span"> details </summary>

Flush all cache on the server immediately

# Example

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
            srv.flush();
        }
    ],
}
```
</details>

</div>
</br>

<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> get </h2>

```rust,ignore
fn get(cache: Cache, key: String) -> ?
```

<details>
<summary markdown="span"> details </summary>

Get something from the server.

# Args

* `key` - The key you want to get the value from

# Return

A rhai::Dynamic with the value inside

# Example

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
            const client_ip = srv.get("client_ip");
            log("info", `ip of my client is: ${client_ip}`);
        }
    ],
}
```
</details>

</div>
</br>

<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> get_with_cas </h2>

```rust,ignore
fn get_with_cas(cache: Cache, key: String) -> ?
```

<details>
<summary markdown="span"> details </summary>

Get something from the server.

# Args

* `key` - The key you want to get the value from

# Return

A rhai::Dynamic with the value inside

# Example

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
            const client_ip = srv.get("client_ip");
            log("info", `ip of my client is: ${client_ip}`);
        }
    ],
}
```
</details>

</div>
</br>

<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> gets </h2>

```rust,ignore
fn gets(cache: Cache, keys: Array) -> ?
```

<details>
<summary markdown="span"> details </summary>

Gets multiple value from mutliple key from the server.

# Args

* `keys` - The keys you want to get the values from

# Return

A rhai::Map<String, rhai::Dynamic> with the values inside

# Example

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
            const client_ips = srv.gets(["client1_ip", "client2_ip", "client3_ip"]);
            log("info", `client 1: ${client_ips["client1_ip"]}`);
            log("info", `client 2: ${client_ips["client2_ip"]}`);
            log("info", `client 3: ${client_ips["client3_ip"]}`);
        }
    ],
}
```
</details>

</div>
</br>

<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> increment </h2>

```rust,ignore
fn increment(cache: Cache, key: String, value: int) -> ()
```

<details>
<summary markdown="span"> details </summary>

Increment value of the specified key.

# Args

* `key` - The key you want the value to be incremented
* `value` - Amount of the increment

# Example

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
            srv.set("nb_of_client", 1, 0);
            srv.increment("nb_of_client", 21);
            const nb_of_client = srv.get("nb_of_client");
            log("info", `nb of client is: ${nb_of_client}`);
        }
    ],
}
```
</details>

</div>
</br>

<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> prepend </h2>

```rust,ignore
fn prepend(cache: Cache, key: String, value: ?) -> ()
```

<details>
<summary markdown="span"> details </summary>

Prepend value to the key.

# Args

* `key` - The key you want to prepend with the value
* `value` - The value you want to prepend

# Example

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
            srv.set("client_ip", ".0.0", 0);
            // Will get an error if the key doesn't exist
            srv.prepend("client_ip", "0.0");
            const client_ip = srv.get("client_ip");
            log("info", `ip of my client is: ${client_ip}`);
        }
    ],
}
```
</details>

</div>
</br>

<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> replace </h2>

```rust,ignore
fn replace(cache: Cache, key: String, value: ?, duration: int) -> ()
```

<details>
<summary markdown="span"> details </summary>

Replace a key with associate value into memcached server with expiration seconds.

# Args

* `key` - The key you want to replace with the value
* `value` - The value you want to store
* `duration` - The duration time you want the value to remain in cache

# Example

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
            srv.set("client_ip", "0.0.0.0", 0);
            // Will get an error if the key doesn't exist
            srv.replace("client_ip", "255.255.255.255", 0);
            const client_ip = srv.get("client_ip");
            log("info", `ip of my client is: ${client_ip}`);
        }
    ],
}
```
</details>

</div>
</br>

<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> set </h2>

```rust,ignore
fn set(cache: Cache, key: String, value: ?, duration: int) -> ()
```

<details>
<summary markdown="span"> details </summary>

Gets multiple value from mutliple key from the server.

# Args

* `keys` - The keys you want to get the values from

# Return

A rhai::Map<String, rhai::Dynamic> with the values inside

# Example

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
            const client_ips = srv.gets(["client1_ip", "client2_ip", "client3_ip"]);
            log("info", `client 1: ${client_ips["client1_ip"]}`);
            log("info", `client 2: ${client_ips["client2_ip"]}`);
            log("info", `client 3: ${client_ips["client3_ip"]}`);
        }
    ],
}
```
Set a value with its associate key into the server with expiration seconds.

# Args

* `key` - The key you want to allocate with the value
* `value` - The value you want to store
* `duration` - The duration time you want the value to remain in cache

# Example

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
            srv.set("client_ip", "0.0.0.0", 0);
            const client_ip = srv.get("client_ip");
            log("info", `ip of my client is: ${client_ip}`);
        }
    ],
}
```
</details>

</div>
</br>

<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> stats </h2>

```rust,ignore
fn stats(cache: Cache) -> String
```

<details>
<summary markdown="span"> details </summary>

Only for debugging purposes, get all server's statistics in a formatted string

# Return

A formatted string

# Example

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
            const stats = srv.stats();
            log("info", stats);
        }
    ],
}
```
</details>

</div>
</br>

<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> touch </h2>

```rust,ignore
fn touch(cache: Cache, key: String, duration: int) -> ()
```

<details>
<summary markdown="span"> details </summary>

Set a new expiration time for a exist key.

# Args

* `key` - The key you want to change the expiration time
* `duration` - Amount of expiration time

# Example

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
            srv.set("nb_of_client", 21, 5000);
            srv.touch("nb_of_client", 0);
            const nb_of_client = srv.get("nb_of_client");
            log("info", `nb of client is: ${nb_of_client}`);
        }
    ],
}
```
</details>

</div>
</br>
