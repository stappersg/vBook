# global::utils

Utility functions to interact with the system.



<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> get_root_domain </h2>

```rust,ignore
fn get_root_domain(domain: SharedObject) -> String
fn get_root_domain(domain: String) -> String
```

<details>
<summary markdown="span"> details </summary>

Get the root domain (the registrable part)

# Examples

`foo.bar.example.com` => `example.com`
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> hostname </h2>

```rust,ignore
fn hostname() -> String
```

<details>
<summary markdown="span"> details </summary>

Get the hostname of this machine.

### Return

* `string` - the host name of the machine.

### Effective smtp stage

All of them.

### Examples

```
#{
  connect: [
    rule "hostname" || {
      state::accept(`250 ${utils::hostname()}`);
    }
  ]
}
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> user_exist </h2>

```rust,ignore
fn user_exist(name: String) -> bool
fn user_exist(name: SharedObject) -> bool
```

<details>
<summary markdown="span"> details </summary>

Check if a user exists on this server.

### Args

* `name` - the name of the user.

### Return

* `bool` - true if the user exists, false otherwise.

### Effective smtp stage

All of them.

### Examples

```
#{
  connect: [
    rule "user_exist" || {
      state::accept(`250 root exist ? ${if utils::user_exist("root") { "yes" } else { "no" }}`);
    }
  ],
  mail: [
    rule "user_exist (obj)" || {
      state::accept(`250 ${utils::user_exist(ctx::mail_from())}`);
    }
  ]
}
```
</details>

</div>
</br>

