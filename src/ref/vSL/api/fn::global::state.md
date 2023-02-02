# global::state

Functions used to interact with the rule engine.
Use `states` in `rules` to deny, accept, or quarantine emails.


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>op</code> != </h2>

```rust,ignore
op !=(status_1: Status, status_2: Status) -> bool
```

<details>
<summary markdown="span"> details </summary>

Operator `!=` for `Status`
</details>

</div>
</br>

<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>op</code> == </h2>

```rust,ignore
op ==(status_1: Status, status_2: Status) -> bool
```

<details>
<summary markdown="span"> details </summary>

Operator `==` for `Status`
</details>

</div>
</br>

<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> accept </h2>

```rust,ignore
fn accept() -> Status
fn accept(code: SharedObject) -> Status
fn accept(code: String) -> Status
```

<details>
<summary markdown="span"> details </summary>

Tell the rule engine to accept the incoming transaction for the current stage.
This means that all rules following the one `accept` is called in the current stage
will be ignored.

# Effective smtp stage

all of them.

# Example

```ignore
#{
    connect: [
        // "ignored checks" will be ignored because the previous rule returned accept.
        rule "accept" || state::accept(),
        action "ignore checks" || print("this will be ignored because the previous rule used state::accept()."),
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

<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> deny </h2>

```rust,ignore
fn deny() -> Status
fn deny(code: SharedObject) -> Status
fn deny(code: String) -> Status
```

<details>
<summary markdown="span"> details </summary>

Stop rules evaluation and/or send an error code to the client.
The code sent is `554 - permanent problems with the remote server`.

To use a custom code, see `deny(code)`.

# Effective smtp stage

all of them.

# Example

```ignore
#{
    rcpt: [
        rule "check for satan" || {
           // The client is denied if a recipient's domain matches satan.org,
           // this is a blacklist, sort-of.
           if ctx::rcpt().domain == "satan.org" {
               state::deny()
           } else {
               state::next()
           }
       },
    ],
}
```
</details>

</div>
</br>

<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> faccept </h2>

```rust,ignore
fn faccept() -> Status
fn faccept(code: SharedObject) -> Status
fn faccept(code: String) -> Status
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

```ignore
#{
    connect: [
        // Here we imagine that "192.168.1.10" is a trusted source, so we can force accept
        // any other rules that don't need to be run.
        rule "check for trusted source" || if ctx::client_ip() == "192.168.1.10" { faccept() } else { state::next() },
    ],

    // The following rules will not be evaluated if `ctx::client_ip() == "192.168.1.10"` is true.
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

<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> next </h2>

```rust,ignore
fn next() -> Status
```

<details>
<summary markdown="span"> details </summary>

Tell the rule engine that a rule succeeded. Following rules
in the current stage will be executed.

# Effective smtp stage

all of them.

# Example

```ignore
#{
    connect: [
        // once "go to the next rule" is evaluated, the rule engine execute "another rule".
        rule "go to the next rule" || state::next(),
        action "another rule" || print("checking stuff ..."),
    ],
}
```
</details>

</div>
</br>

<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> quarantine </h2>

```rust,ignore
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

```ignore
import "services" as svc;

#{
    postq: [
          delegate svc::clamsmtpd "check email for virus" || {
              // the email is placed in quarantined if a virus is detected by
              // a service.
              if has_header("X-Virus-Infected") {
                state::quarantine("virus_queue")
              } else {
                state::next()
              }
          }
    ],
}
```
</details>

</div>
</br>

<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> to_debug </h2>

```rust,ignore
fn to_debug(status: Status) -> String
```

<details>
<summary markdown="span"> details </summary>

Convert a `Status` to a debug string
</details>

</div>
</br>

<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> to_string </h2>

```rust,ignore
fn to_string(status: Status) -> String
```

<details>
<summary markdown="span"> details </summary>

Convert a `Status` to a `String`
</details>

</div>
</br>
