# global::rule_state



<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn accept() -> Status
```

<details>
<summary markdown="span"> details </summary>

Tell the rule engine to accept the incoming transaction for the current stage.
This means that all rules following the one `accept` is called in the current stage
will be ignored.

# Effective smtp stage

all of them.

# Example

```
#{
    connect: [
        // "ignored checks" will be ignored because the previous rule returned accept.
        rule "accept" || accept(),
        action "ignore checks" || print("this will be ignored because the previous rule used accept()."),
    ],

    mail: [
        // rule evaluation is resumed in the next stage.
        rule "resume rules" || print("evaluation resumed!");
    ]
}
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn accept(code: String) -> Status
```

<details>
<summary markdown="span"> details </summary>

Tell the rule engine to accept the incoming transaction for the current stage.
This means that all rules following the one `accept` is called in the current stage
will be ignored.

# Args

* `code` - A custom code as a string to send to the client.

# Error

* Could not parse the parameter as a valid SMTP reply code.

# Effective smtp stage

all of them.

# Example

```
#{
    connect: [
        // "ignored checks" will be ignored because the previous rule returned accept.
        rule "accept" || accept(code(220, "Ok")),
        action "ignore checks" || print("this will be ignored because the previous rule used accept()."),
    ],

    mail: [
        // rule evaluation is resumed in the next stage.
        rule "resume rules" || print("evaluation resumed!");
    ]
}
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn accept(code: SharedObject) -> Status
```

<details>
<summary markdown="span"> details </summary>

Tell the rule engine to accept the incoming transaction for the current stage.
This means that all rules following the one `accept` is called in the current stage
will be ignored.

# Args

* `code` - A custom code using a `code` object to send to the client.

# Error

* The given parameter was not a code object.

# Effective smtp stage

all of them.

# Example

```
#{
    connect: [
        // "ignored checks" will be ignored because the previous rule returned accept.
        rule "accept" || accept(code(220, "Ok")),
        action "ignore checks" || print("this will be ignored because the previous rule used accept()."),
    ],

    mail: [
        // rule evaluation is resumed in the next stage.
        rule "resume rules" || print("evaluation resumed!");
    ]
}
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn deny() -> Status
```

<details>
<summary markdown="span"> details </summary>

Stop rules evaluation and/or send an error code to the client.
The code sent is `554 - permanent problems with the remote server`.

To use a custom code, see `deny(code)`.

# Effective smtp stage

all of them.

# Example

```
#{
    rcpt: [
        rule "check for satan" || {
           // The client is denied if a recipient's domain matches satan.org,
           // this is a blacklist, sort-of.
           if rcpt().domain == "satan.org" {
               deny()
           } else {
               next()
           }
       },
    ],
}
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn deny(code: String) -> Status
```

<details>
<summary markdown="span"> details </summary>

Stop rules evaluation and/or send an error code to the client.

# Args

* `code` - A custom code as a string to send to the client.

# Error

* Could not parse the parameter as a valid SMTP reply code.

# Effective smtp stage

all of them.

# Example

```
#{
    rcpt: [
        rule "check for satan" || {
           // The client is denied if a recipient's domain matches satan.org,
           // this is a blacklist, sort-of.
           if rcpt().domain == "satan.org" {
               deny("554 permanent problems with the remote server")
           } else {
               next()
           }
       },
    ],
}
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn deny(code: SharedObject) -> Status
```

<details>
<summary markdown="span"> details </summary>

Stop rules evaluation and/or send an error code to the client.

# Args

* `code` - A custom code using a `code` object to send to the client.
           See `code()` for more information.

# Error

* The given parameter was not a code object.

# Effective smtp stage

all of them.

# Example

```
#{
    rcpt: [
        rule "check for satan" || {
           // The client is denied if a recipient's domain matches satan.org,
           // this is a blacklist, sort-of.
           if rcpt().domain == "satan.org" {
               deny(code(554, "permanent problems with the remote server"))
           } else {
               next()
           }
       },
    ],
}
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn faccept() -> Status
```

<details>
<summary markdown="span"> details </summary>

Tell the rule engine to force accept the incoming transaction.
This means that all rules following the one `faccept` is called
will be ignored.

Sends an 'Ok' code to the client. To customize the code to send,
see `faccept(code)`.

Use this return status when you are sure that
the incoming client can be trusted.

# Effective smtp stage

all of them.

# Example

```
#{
    connect: [
        // Here we imagine that "192.168.1.10" is a trusted source, so we can force accept
        // any other rules that don't need to be run.
        rule "check for trusted source" || if client_ip() == "192.168.1.10" { faccept() } else { next() },
    ],

    // The following rules will not be evaluated if `client_ip() == "192.168.1.10"` is true.
    mail: [
        rule "another rule" || {
            // ... doing stuff
        }
    ],
}
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn faccept(code: String) -> Status
```

<details>
<summary markdown="span"> details </summary>

Tell the rule engine to force accept the incoming transaction.
This means that all rules following the one `faccept` is called
will be ignored.

Use this return status when you are sure that
the incoming client can be trusted.

# Args

* `code` - a custom code as a string to send to the client.

# Error

* Could not parse the parameter as a valid SMTP reply code.

# Effective smtp stage

all of them.

# Example
```
#{
    connect: [
        // Here we imagine that "192.168.1.10" is a trusted source, so we can force accept
        // any other rules that don't need to be run.
        rule "check for trusted source" || if client_ip() == "192.168.1.10" { faccept("220 Ok") } else { next() },
    ],

    // The following rules will not be evaluated if `client_ip() == "192.168.1.10"` is true.
    mail: [
        rule "another rule" || {
            // ... doing stuff
        }
    ],
}
```

# Errors
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn faccept(code: SharedObject) -> Status
```

<details>
<summary markdown="span"> details </summary>

Tell the rule engine to force accept the incoming transaction.
This means that all rules following the one `faccept` is called
will be ignored.

Use this return status when you are sure that
the incoming client can be trusted.

# Args

* `code` - a custom code using a `code` object to send to the client.

# Error

* The given parameter was not a code object.

# Effective smtp stage

all of them.

# Example

```
#{
    connect: [
        // Here we imagine that "192.168.1.10" is a trusted source, so we can force accept
        // any other rules that don't need to be run.
        rule "check for trusted source" || if client_ip() == "192.168.1.10" { faccept(code(220, "Ok")) } else { next() },
    ],

    // The following rules will not be evaluated if `client_ip() == "192.168.1.10"` is true.
    mail: [
        rule "another rule" || {
            // ... doing stuff
        }
    ],
}
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn info(code: String) -> Status
```

<details>
<summary markdown="span"> details </summary>

Ask the client to retry to send the current command by sending an information code.

# Args

* `code` - A custom code as a string to send to the client.

# Error

* Could not parse the parameter as a valid SMTP reply code.

# Effective smtp stage

all of them.

# Example

```
#{
    connect: [
        rule "please retry" || {
           info("451 failed to understand you request, please retry")
       },
    ],
}
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn info(code: SharedObject) -> Status
```

<details>
<summary markdown="span"> details </summary>

Ask the client to retry to send the current command by sending an information code.

# Args

* `code` - A custom code using a `code` object to send to the client.
           See `code()` for more information.

# Error

* The given parameter was not a code object.

# Effective smtp stage

all of them.

# Example

```
#{
    connect: [
        rule "please retry" || {
           const info_code = code(451, "failed to understand you request, please retry.");
           info(info_code)
       },
    ],
}
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn next() -> Status
```

<details>
<summary markdown="span"> details </summary>

Tell the rule engine that a rule succeeded. Following rules
in the current stage will be executed.

# Effective smtp stage

all of them.

# Example

```
#{
    connect: [
        // once "go to the next rule" is evaluated, the rule engine execute "another rule".
        rule "go to the next rule" || next(),
        action "another rule" || print("checking stuff ..."),
    ],
}
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn quarantine(queue: String) -> Status
```

<details>
<summary markdown="span"> details </summary>

Skip all rules until the email is received and place the email in a
quarantine queue. The email will never be sent to the recipients and
will stop being processed after the `PreQ` stage.

# Args

* `queue` - the relative path to the queue where the email will be quarantined as a string.
            This path will be concatenated to the `config.app.dirpath` field in
            your root configuration.

# Effective smtp stage

all of them.

# Example

```
import "services" as svc;

#{
    postq: [
          delegate svc::clamsmtpd "check email for virus" || {
              // the email is placed in quarantined if a virus is detected by
              // a service.
              if has_header("X-Virus-Infected") {
                quarantine("virus_queue")
              } else {
                next()
              }
          }
    ],
}
```
</details>

</div>
</br>

