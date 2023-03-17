# global::state

Functions used to interact with the rule engine.
Use `states` in `rules` to deny, accept, or quarantine emails.


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> faccept </h2>

```rust,ignore
fn faccept() -> Status
fn faccept(code: String) -> Status
fn faccept(code: SharedObject) -> Status
```

<div class="tab">
    <button
    group="faccept"
    id="link-faccept-description"
    class="tablinks active"
    onclick="openTab(event, 'faccept', 'description')">
        Description
    </button>
    <button
    group="faccept"
    id="link-faccept-Args"
    class="tablinks"
    onclick="openTab(event, 'faccept', 'Args')">
        Args
    </button>
    <button
    group="faccept"
    id="link-faccept-Errors"
    class="tablinks"
    onclick="openTab(event, 'faccept', 'Errors')">
        Errors
    </button>
    <button
    group="faccept"
    id="link-faccept-Effective smtp stage"
    class="tablinks"
    onclick="openTab(event, 'faccept', 'Effective smtp stage')">
        Effective smtp stage
    </button>
    <button
    group="faccept"
    id="link-faccept-Example"
    class="tablinks"
    onclick="openTab(event, 'faccept', 'Example')">
        Example
    </button></div>

<div group="faccept" id="faccept-description" style="display: block;" markdown="span" class="tabcontent">
Tell the rule engine to force accept the incoming transaction.
This means that all rules following the one `faccept` is called
will be ignored.

Use this return status when you are sure that
the incoming client can be trusted.


</div>

<div group="faccept" id="faccept-Args" class="tabcontent">
   
* code - A customized code as a string or code object. (default: "250 Ok")


</div>

<div group="faccept" id="faccept-Errors" class="tabcontent">

* The object passed as parameter was not a code object.
* The string passed as parameter failed to be parsed into a valid code.


</div>

<div group="faccept" id="faccept-Effective smtp stage" class="tabcontent">

all of them.


</div>

<div group="faccept" id="faccept-Example" class="tabcontent">

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

#{
    mail: [
        rule "send a custom code with a code object" || {
            faccept(code(220, "Ok"))
        }
    ],
}

#{
    mail: [
        rule "send a custom code with a string" || {
            faccept("220 Ok")
        }
    ],
}
```
</div>

</div>
</br>

<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> accept </h2>

```rust,ignore
fn accept() -> Status
fn accept(code: SharedObject) -> Status
fn accept(code: String) -> Status
```

<div class="tab">
    <button
    group="accept"
    id="link-accept-description"
    class="tablinks active"
    onclick="openTab(event, 'accept', 'description')">
        Description
    </button>
    <button
    group="accept"
    id="link-accept-Args"
    class="tablinks"
    onclick="openTab(event, 'accept', 'Args')">
        Args
    </button>
    <button
    group="accept"
    id="link-accept-Errors"
    class="tablinks"
    onclick="openTab(event, 'accept', 'Errors')">
        Errors
    </button>
    <button
    group="accept"
    id="link-accept-Effective smtp stage"
    class="tablinks"
    onclick="openTab(event, 'accept', 'Effective smtp stage')">
        Effective smtp stage
    </button>
    <button
    group="accept"
    id="link-accept-Example"
    class="tablinks"
    onclick="openTab(event, 'accept', 'Example')">
        Example
    </button></div>

<div group="accept" id="accept-description" style="display: block;" markdown="span" class="tabcontent">
Tell the rule engine to accept the incoming transaction for the current stage.
This means that all rules following the one `accept` is called in the current stage
will be ignored.


</div>

<div group="accept" id="accept-Args" class="tabcontent">
   
* code - A customized code as a string or code object. (default: "250 Ok")


</div>

<div group="accept" id="accept-Errors" class="tabcontent">

* The object passed as parameter was not a code object.
* The string passed as parameter failed to be parsed into a valid code.


</div>

<div group="accept" id="accept-Effective smtp stage" class="tabcontent">

all of them.


</div>

<div group="accept" id="accept-Example" class="tabcontent">

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

#{
    mail: [
        rule "send a custom code with a code object" || {
            accept(code(220, "Ok"))
        }
    ],
}

#{
    mail: [
        rule "send a custom code with a string" || {
            accept("220 Ok")
        }
    ],
}
```
</div>

</div>
</br>

<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> next </h2>

```rust,ignore
fn next() -> Status
```

<div class="tab">
    <button
    group="next"
    id="link-next-description"
    class="tablinks active"
    onclick="openTab(event, 'next', 'description')">
        Description
    </button>
    <button
    group="next"
    id="link-next-Effective smtp stage"
    class="tablinks"
    onclick="openTab(event, 'next', 'Effective smtp stage')">
        Effective smtp stage
    </button>
    <button
    group="next"
    id="link-next-Example"
    class="tablinks"
    onclick="openTab(event, 'next', 'Example')">
        Example
    </button></div>

<div group="next" id="next-description" style="display: block;" markdown="span" class="tabcontent">
Tell the rule engine that a rule succeeded. Following rules
in the current stage will be executed.


</div>

<div group="next" id="next-Effective smtp stage" class="tabcontent">

all of them.


</div>

<div group="next" id="next-Example" class="tabcontent">

```ignore
#{
    connect: [
        // once "go to the next rule" is evaluated, the rule engine execute "another rule".
        rule "go to the next rule" || state::next(),
        action "another rule" || print("checking stuff ..."),
    ],
}
```
</div>

</div>
</br>

<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> deny </h2>

```rust,ignore
fn deny() -> Status
fn deny(code: String) -> Status
fn deny(code: SharedObject) -> Status
```

<div class="tab">
    <button
    group="deny"
    id="link-deny-description"
    class="tablinks active"
    onclick="openTab(event, 'deny', 'description')">
        Description
    </button>
    <button
    group="deny"
    id="link-deny-Args"
    class="tablinks"
    onclick="openTab(event, 'deny', 'Args')">
        Args
    </button>
    <button
    group="deny"
    id="link-deny-Errors"
    class="tablinks"
    onclick="openTab(event, 'deny', 'Errors')">
        Errors
    </button>
    <button
    group="deny"
    id="link-deny-Effective smtp stage"
    class="tablinks"
    onclick="openTab(event, 'deny', 'Effective smtp stage')">
        Effective smtp stage
    </button>
    <button
    group="deny"
    id="link-deny-Example"
    class="tablinks"
    onclick="openTab(event, 'deny', 'Example')">
        Example
    </button></div>

<div group="deny" id="deny-description" style="display: block;" markdown="span" class="tabcontent">
Stop rules evaluation and send an error code to the client.


</div>

<div group="deny" id="deny-Args" class="tabcontent">
   
* code - A customized code as a string or code object. (default: "554 permanent problems with the remote server")


</div>

<div group="deny" id="deny-Errors" class="tabcontent">

* The object passed as parameter was not a code object.
* The string passed as parameter failed to be parsed into a valid code.


</div>

<div group="deny" id="deny-Effective smtp stage" class="tabcontent">

all of them.


</div>

<div group="deny" id="deny-Example" class="tabcontent">

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

#{
    mail: [
        rule "send a custom code with a code object" || {
            deny(code(421, "Service not available"))
        }
    ],
}

#{
    mail: [
        rule "send a custom code with a string" || {
            deny("450 mailbox unavailable")
        }
    ],
}
```
</div>

</div>
</br>

<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> quarantine </h2>

```rust,ignore
fn quarantine(queue: String) -> Status
```

<div class="tab">
    <button
    group="quarantine"
    id="link-quarantine-description"
    class="tablinks active"
    onclick="openTab(event, 'quarantine', 'description')">
        Description
    </button>
    <button
    group="quarantine"
    id="link-quarantine-Args"
    class="tablinks"
    onclick="openTab(event, 'quarantine', 'Args')">
        Args
    </button>
    <button
    group="quarantine"
    id="link-quarantine-Effective smtp stage"
    class="tablinks"
    onclick="openTab(event, 'quarantine', 'Effective smtp stage')">
        Effective smtp stage
    </button>
    <button
    group="quarantine"
    id="link-quarantine-Example"
    class="tablinks"
    onclick="openTab(event, 'quarantine', 'Example')">
        Example
    </button></div>

<div group="quarantine" id="quarantine-description" style="display: block;" markdown="span" class="tabcontent">
Skip all rules until the email is received and place the email in a
quarantine queue. The email will never be sent to the recipients and
will stop being processed after the `PreQ` stage.


</div>

<div group="quarantine" id="quarantine-Args" class="tabcontent">

* `queue` - the relative path to the queue where the email will be quarantined as a string.
            This path will be concatenated to the `config.app.dirpath` field in
            your root configuration.


</div>

<div group="quarantine" id="quarantine-Effective smtp stage" class="tabcontent">

all of them.


</div>

<div group="quarantine" id="quarantine-Example" class="tabcontent">

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
</div>

</div>
</br>

<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>op</code> == </h2>

```rust,ignore
op ==(status_1: Status, status_2: Status) -> bool
```

<div class="tab">
    <button
    group="=="
    id="link-==-description"
    class="tablinks active"
    onclick="openTab(event, '==', 'description')">
        Description
    </button>
    <button
    group="=="
    id="link-==-Effective smtp stage"
    class="tablinks"
    onclick="openTab(event, '==', 'Effective smtp stage')">
        Effective smtp stage
    </button>
    <button
    group="=="
    id="link-==-Example"
    class="tablinks"
    onclick="openTab(event, '==', 'Example')">
        Example
    </button></div>

<div group="==" id="==-description" style="display: block;" markdown="span" class="tabcontent">
Check if two statuses are equal.


</div>

<div group="==" id="==-Effective smtp stage" class="tabcontent">

all of them.


</div>

<div group="==" id="==-Example" class="tabcontent">

```ignore
#{
    connect: [
        action "check status equality" || {
            deny() == deny(); // returns true.
            faccept() == next(); // returns false.
        }
    ],
}
```
</div>

</div>
</br>

<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>op</code> != </h2>

```rust,ignore
op !=(status_1: Status, status_2: Status) -> bool
```

<div class="tab">
    <button
    group="!="
    id="link-!=-description"
    class="tablinks active"
    onclick="openTab(event, '!=', 'description')">
        Description
    </button>
    <button
    group="!="
    id="link-!=-Effective smtp stage"
    class="tablinks"
    onclick="openTab(event, '!=', 'Effective smtp stage')">
        Effective smtp stage
    </button>
    <button
    group="!="
    id="link-!=-Example"
    class="tablinks"
    onclick="openTab(event, '!=', 'Example')">
        Example
    </button></div>

<div group="!=" id="!=-description" style="display: block;" markdown="span" class="tabcontent">
Check if two statuses are not equal.


</div>

<div group="!=" id="!=-Effective smtp stage" class="tabcontent">

all of them.


</div>

<div group="!=" id="!=-Example" class="tabcontent">

```ignore
#{
    connect: [
        action "check status not equal" || {
            deny() != deny(); // returns false.
            faccept() != next(); // returns true.
        }
    ],
}
```
</div>

</div>
</br>

<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> to_string </h2>

```rust,ignore
fn to_string(status: Status) -> String
```

<div class="tab">
    <button
    group="to_string"
    id="link-to_string-description"
    class="tablinks active"
    onclick="openTab(event, 'to_string', 'description')">
        Description
    </button>
    <button
    group="to_string"
    id="link-to_string-Effective smtp stage"
    class="tablinks"
    onclick="openTab(event, 'to_string', 'Effective smtp stage')">
        Effective smtp stage
    </button>
    <button
    group="to_string"
    id="link-to_string-Example"
    class="tablinks"
    onclick="openTab(event, 'to_string', 'Example')">
        Example
    </button></div>

<div group="to_string" id="to_string-description" style="display: block;" markdown="span" class="tabcontent">
Convert a status to a string.
Enables string interpolation.


</div>

<div group="to_string" id="to_string-Effective smtp stage" class="tabcontent">

all of them.


</div>

<div group="to_string" id="to_string-Example" class="tabcontent">

```text,ignore
#{
    connect: [
        rule "status to string" || {
            let status = next();
            // `.to_string` is called automatically here.
            log("info", `converting my status to a string: ${status}`);
            status
        }
    ],
}
```
</div>

</div>
</br>

<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> to_debug </h2>

```rust,ignore
fn to_debug(status: Status) -> String
```

<div class="tab">
    <button
    group="to_debug"
    id="link-to_debug-description"
    class="tablinks active"
    onclick="openTab(event, 'to_debug', 'description')">
        Description
    </button>
    <button
    group="to_debug"
    id="link-to_debug-Effective smtp stage"
    class="tablinks"
    onclick="openTab(event, 'to_debug', 'Effective smtp stage')">
        Effective smtp stage
    </button>
    <button
    group="to_debug"
    id="link-to_debug-Example"
    class="tablinks"
    onclick="openTab(event, 'to_debug', 'Example')">
        Example
    </button></div>

<div group="to_debug" id="to_debug-description" style="display: block;" markdown="span" class="tabcontent">
Convert a status to a debug string
Enables string interpolation.


</div>

<div group="to_debug" id="to_debug-Effective smtp stage" class="tabcontent">

all of them.


</div>

<div group="to_debug" id="to_debug-Example" class="tabcontent">

```text,ignore
#{
    connect: [
        rule "status to string" || {
            let status = next();
            log("info", `converting my status to a string: ${status.to_debug()}`);
            status
        }
    ],
}
```
</div>

</div>
</br>
