# global::utils



<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> date </h2>

```rust,ignore
fn date() -> String

```

<details>
<summary markdown="span"> details </summary>

Get the current date.

### Return

* `string` - the current date.

### Effective smtp stage

All of them.

### Examples

```rust,ignore
#{
    preq: [
       action "append info header" || {
            append_header("X-VSMTP", `email received by ${hostname()} the ${date()}.`);
       }
    ]
}
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> get_root_domain </h2>

```rust,ignore
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

<h2 class="func-name"> <code>fn</code> lookup </h2>

```rust,ignore
fn lookup(server: Server, name: String) -> Array
fn lookup(server: Server, name: SharedObject) -> Array
```

<details>
<summary markdown="span"> details </summary>

Performs a dual-stack DNS lookup for the given hostname.

### Args

* `host` - A valid hostname to search.

### Return

* `array` - an array of IPs. The array is empty if no IPs were found for the host.

### Effective smtp stage

All of them.

# Errors

* Root resolver was not found.
* Lookup failed.

### Examples

```
#{
    rcpt: [
       action "perform lookup" || {
            let domain = rcpt().domain;
            let ips = lookup(domain);

            print(`ips found for ${domain}`);
            for ip in ips {
                print(`- ${ip}`);
            }
       }
    ]
}
```

```rust,ignore
# vsmtp_test::vsl::run(
# |builder| Ok(builder.add_root_incoming_rules(r#"
#{
  preq: [
    action "lookup recipients" || {
      let domain = "gmail.com";
      let ips = lookup(domain);

      print(`ips found for ${domain}`);
      for ip in ips { print(`- ${ip}`); }
    },
  ],
}
# "#)?.build()));
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> rlookup </h2>

```rust,ignore
fn rlookup(server: Server, name: SharedObject) -> Array

```

<details>
<summary markdown="span"> details </summary>

Performs a reverse lookup for the given IP.

### Args

* `ip` - The IP to query.

### Return

* `array` - an array of FQDNs. The array is empty if nothing was found.

### Effective smtp stage

All of them.

# Errors

* Failed to convert the `ip` parameter from a string into an IP.
* Reverse lookup failed.

### Examples

```rust,ignore
#{
    connect: [
       action "perform reverse lookup" || {
            let domains = rlookup(client_ip());

            print(`domains found for ip ${client_ip()}`);
            for domain in domains {
                print(`- ${domain}`);
            }
       }
    ]
}
```

```
# let states = vsmtp_test::vsl::run(
# |builder| Ok(builder.add_root_incoming_rules(r#"
#{
  connect: [
    rule "rlookup" || {
      accept(`250 client ip: ${"127.0.0.1"} -> ${rlookup("127.0.0.1")}`);
    }
  ],
}
# "#)?.build()));
# use vsmtp_common::{status::Status, CodeID, Reply, ReplyCode::Code};
# assert_eq!(states[&vsmtp_rule_engine::ExecutionStage::Connect].2, Status::Accept(either::Right(Reply::new(
#  Code { code: 250 }, "client ip: 127.0.0.1 -> [\"localhost.\"]".to_string(),
# ))));
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> user_exist </h2>

```rust,ignore
fn user_exist(name: SharedObject) -> bool
fn user_exist(name: String) -> bool
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

```rust,ignore
#{
    rcpt: [
       action "check for local user" || {
           if user_exist(rcpt().local_part) {
               log("debug", `${rcpt().local_part} exists on disk.`);
           }
       }
    ]
}
```

```
# let states = vsmtp_test::vsl::run(
# |builder| Ok(builder.add_root_incoming_rules(r#"
#{
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
# "#)?.build()));
# use vsmtp_common::{status::Status, CodeID, Reply, ReplyCode::Code};
# assert_eq!(states[&vsmtp_rule_engine::ExecutionStage::Connect].2, Status::Accept(either::Right(Reply::new(
#  Code { code: 250 }, "root exist ? yes".to_string(),
# ))));
# assert_eq!(states[&vsmtp_rule_engine::ExecutionStage::MailFrom].2, Status::Accept(either::Right(Reply::new(
#  Code { code: 250 }, "false".to_string(),
# ))));
```
</details>

</div>
</br>

