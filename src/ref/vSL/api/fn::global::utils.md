# global::utils



<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn date() -> String
```

<details>
<summary markdown="span"> details </summary>

get the current date.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn get_root_domain(domain: SharedObject) -> String
```

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
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


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn hostname() -> String
```

<details>
<summary markdown="span"> details </summary>

Get the hostname of the machine.

# Examples

```
  connect: [
    rule "hostname" || {
      accept(`250 ${hostname()}`);
    }
  ]
}
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn lookup(server: Server, name: String) -> Array
```

<details>
<summary markdown="span"> details </summary>

Perform a dns lookup using the root dns.

# Errors

* Root resolver was not found.
* Lookup failed.

# Examples

```
  preq: [
    action "lookup recipients" || {
      let domain = "gmail.com";
      let ips = lookup(domain);

      print(`ips found for ${domain}`);
      for ip in ips { print(`- ${ip}`); }
    },
  ],
}
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn lookup(server: Server, name: SharedObject) -> Array
```

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn rlookup(server: Server, name: String) -> Array
```

<details>
<summary markdown="span"> details </summary>

Perform a dns reverse lookup using the root dns.

# Errors

* Failed to convert the `ip` parameter from a string into an IP.
* Reverse lookup failed.

# Examples

```
  connect: [
    rule "rlookup" || {
      accept(`250 client ip: ${"127.0.0.1"} -> ${rlookup("127.0.0.1")}`);
    }
  ],
}
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn rlookup(server: Server, name: SharedObject) -> Array
```

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn send_mail(from: String, to: Array, path: String, relay: String) -> ()
```

<details>
<summary markdown="span"> details </summary>

send a mail from a template.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn time() -> String
```

<details>
<summary markdown="span"> details </summary>

get the current time.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn user_exist(name: String) -> bool
```

<details>
<summary markdown="span"> details </summary>

Does the `name` correspond to an existing user in the system.

# Examples

```
  connect: [
    rule "user_exist" || {
      accept(`250 root exist ? ${if user_exist("root") { "yes" } else { "no" }}`);
    }
  ],
  mail: [
    rule "user_exist (obj)" || {
      accept(`250 ${user_exist(mail_from())}`);
    }
  ]
}
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn user_exist(name: SharedObject) -> bool
```

</div>
</br>

