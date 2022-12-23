# global::logging

Logging mechanisms.



<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> log </h2>

```rust,ignore
fn log(level: String, message: SharedObject)
fn log(level: SharedObject, message: SharedObject)
fn log(level: SharedObject, message: String)
fn log(level: String, message: String)
```

<details>
<summary markdown="span"> details </summary>

Log information to stdout in `nodaemon` mode or to a file.

# Args

* `level` - the level of the message, can be "trace", "debug", "info", "warn" or "error".
* `message` - the message to log.

# Effective smtp stage

All of them.

# Examples

```
#{
  connect: [
    action "log on connection (str/str)" || {
      log("info", `[${date()}/${time()}] client=${ctx::client_ip()}`);
    },
    action "log on connection (str/obj)" || {
      log("error", identifier("Ehllo world!"));
    },
    action "log on connection (obj/obj)" || {
      const level = "trace";
      const message = "connection established";

      log(identifier(level), identifier(message));
    },
    action "log on connection (obj/str)" || {
      const level = "warn";

      log(identifier(level), "I love vsl!");
    },
  ],
}
```
</details>

</div>
</br>

