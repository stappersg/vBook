# global::logging



<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn log(level: String, message: String)
```

<details>
<summary markdown="span"> details </summary>

# Examples

```
  connect: [
    action "log on connection (str/str)" || {
      log("info", `[${date()}/${time()}] client=${client_ip()}`);
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


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn log(level: String, message: SharedObject)
```

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn log(level: SharedObject, message: String)
```

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn log(level: SharedObject, message: SharedObject)
```

</div>
</br>

