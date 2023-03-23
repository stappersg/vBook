# global::logging

Logging mechanisms.


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> log </h2>

```rust,ignore
fn log(level: SharedObject, message: String)
fn log(level: String, message: SharedObject)
fn log(level: SharedObject, message: SharedObject)
fn log(level: String, message: String)
```

<div class="tab">
    <button
    group="log"
    id="link-log-description"
    class="tablinks active"
    onclick="openTab(event, 'log', 'description')">
        Description
    </button>
    <button
    group="log"
    id="link-log-Args"
    class="tablinks"
    onclick="openTab(event, 'log', 'Args')">
        Args
    </button>
    <button
    group="log"
    id="link-log-Effective smtp stage"
    class="tablinks"
    onclick="openTab(event, 'log', 'Effective smtp stage')">
        Effective smtp stage
    </button>
    <button
    group="log"
    id="link-log-Examples"
    class="tablinks"
    onclick="openTab(event, 'log', 'Examples')">
        Examples
    </button></div>

<div group="log" id="log-description" style="display: block;" markdown="span" class="tabcontent">
Log information to stdout in `nodaemon` mode or to a file.


</div>

<div group="log" id="log-Args" class="tabcontent">

* `level` - the level of the message, can be "trace", "debug", "info", "warn" or "error".
* `message` - the message to log.


</div>

<div group="log" id="log-Effective smtp stage" class="tabcontent">

All of them.


</div>

<div group="log" id="log-Examples" class="tabcontent">

```
#{
  connect: [
    action "log on connection (str/str)" || {
      log("info", `[${date()}/${time()}] client=${ctx::client_ip()}`);
    },
    action "log on connection (str/obj)" || {
      log("error", identifier("Hello world!"));
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
</div>

</div>
</br>
