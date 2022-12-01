# global::vsl-api

//! ### Codes
//!
//! This module contains predefined codes for SMTP responses.
//! ### Networks
//!
//! Standard objects for networking.
//! ### Auth
//!
//! This module contains authentication mechanisms to secure your server.
//! ### Connection
//!
//! Metadata is available for each client, this module lets you query those metadata.
//! ### Delivery
//!
//! Those methods are used to setup the method of delivery for one / every recipient.
//! ### Envelop
//!
//! The SMTP envelop can be mutated by several function from this module.
//! ### Internal
//!
//! A low level api to get access to internal functions of vsl.
//! ### Message
//!
//! Those methods are used to query data from the email and/or mutate it.
//! ### Security
//!
//! This module contains multiple security functions that you can use to protect your server.
//! ### Status
//!
//! The state of an SMTP transaction can be changed through specific functions from this module.
//! ### Transaction
//!
//! At each SMTP stage, data from the client is received via 'SMTP commands'.
//! This module lets you query the content of the commands.
//! ### Utils
//!
//! Those miscellaneous functions lets you query data from your system,
//! log stuff, perform dns lookups etc ...



<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn accept()
```

<details>
<summary markdown="span"> details </summary>

Tell the rule engine to accept the incoming transaction for the current stage.
This means that all rules following the one `accept` is called in the current stage
will be ignored.

### Effective smtp stage

all of them.

### Example
```js
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
fn add_rcpt_envelop(rcpt: ?)
```

<details>
<summary markdown="span"> details </summary>

Add a new recipient to the envelop. Note that this does not add
the recipient to the `To` header. Use `add_rcpt_message` for that.

### Args

* `rcpt` - the new recipient to add.

### Effective smtp stage

All of them.

### Example
```js
#{
    connect: [
       // always deliver a copy of the message to "john.doe@example.com".
       action "rewrite envelop" || add_rcpt_envelop("john.doe@example.com"),
    ]
}
```

</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn add_rcpt_message(addr: ?)
```

<details>
<summary markdown="span"> details </summary>

Add a recipient to the `To` header of the message.

### Args

* `addr` - the recipient address to add to the `To` header.

### Effective smtp stage

`preq` and onwards.

### Example
```js
#{
    preq: [
       action "update recipients" || add_rcpt_message("john.doe@example.com"),
    ]
}
```

</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn append_header(header: ?, value: ?)
```

<details>
<summary markdown="span"> details </summary>

Add a new header at the end of the header list in the message.

### Args

* `header` - the name of the header to append.
* `value` - the value of the header to append.

### Effective smtp stage

All of them. Even though the email is not received at the current stage,
vsmtp stores new headers and will add them on top of the ones received once
the `preq` stage is reached.

### Example
```js
#{
    postq: [
        action "append a header" || {
            append_header("X-JOHN", "received by john's server.");
        }
    ],
}
```

</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn auth()
```

<details>
<summary markdown="span"> details </summary>

Get authentication credentials from the client.

### Effective smtp stage

`authenticate` only.

### Return

* `Credentials` - the credentials of the client.

### Example
```js
#{
    authenticate: [
       action "log info" || log("info", `${auth()}`),
    ]
}
```

</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn authenticate()
```

<details>
<summary markdown="span"> details </summary>

Process the SASL authentication mechanism.

The current implementation support "PLAIN" mechanism, and will call the
`testsaslauthd` program to check the credentials.

The credentials will be verified depending on the mode of `saslauthd`.

A native implementation will be provided in the future.

### Module:Auth
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn bcc(rcpt: ?)
```

<details>
<summary markdown="span"> details </summary>

Add a recipient as a blind carbon copy. The equivalent of `add_rcpt_envelop`.

### Args

* `rcpt` - the recipient to add as a blind carbon copy.

### Effective smtp stage

All of them.

### Example
```js
#{
    connect: [
       // set "john.doe@example.com" as a blind carbon copy.
       action "bcc" || bcc("john.doe@example.com"),
    ]
}
```

</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn check_dmarc()
```

<details>
<summary markdown="span"> details </summary>

Apply the DMARC policy to the mail.

### Effective smtp stage

`preq` and onwards.

### Example

```js
#{
  preq: [
    rule "check dmarc" || { check_dmarc() },
  ]
}
```

</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn check_spf(header: ?)
```

<details>
<summary markdown="span"> details </summary>

Check spf record following the Sender Policy Framework (RFC 7208).
A wrapper with the policy set to "strict" by default.
see https://datatracker.ietf.org/doc/html/rfc7208

### Args

* `header` - "spf" | "auth" | "both" | "none"

### Return
* `deny(code550_7_23 | code451_7_24 | code550_7_24)` - an error occurred during lookup. (returned even when a softfail is received using the "strict" policy)
* `next()` - the operation succeeded.

### Effective smtp stage
`rcpt` and onwards.

### Errors
* The `header` argument is not valid.
* The `policy` argument is not valid.

### Note
`check_spf` only checks for the sender's identity, not the `helo` value.

### Example
```js
#{
    mail: [
       rule "check spf relay" || check_spf(allowed_hosts),
    ]
}

#{
    mail: [
        // if this check succeed, it wil return `next`.
        // if it fails, it might return `deny` with a custom code
        // (X.7.24 or X.7.25 for example)
        //
        // if you want to use the return status, just put the check_spf
        // function on the last line of your rule.
        rule "check spf 1" || {
            log("debug", `running sender policy framework on ${mail_from()} identity ...`);
            check_spf("spf", "soft")
        },

        // policy is set to "strict" by default.
        rule "check spf 2" || check_spf("both"),
    ],
}
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn check_spf(header: ?, policy: ?)
```

<details>
<summary markdown="span"> details </summary>

Check spf record following the Sender Policy Framework (RFC 7208).
see https://datatracker.ietf.org/doc/html/rfc7208

### Args

* `header` - "spf" | "auth" | "both" | "none"
* `policy` - "strict" | "soft"

### Return
* `deny(code550_7_23 | code451_7_24 | code550_7_24)` - an error occurred during lookup. (returned even when a softfail is received using the "strict" policy)
* `next()` - the operation succeeded.

### Effective smtp stage
`rcpt` and onwards.

### Errors
* The `header` argument is not valid.
* The `policy` argument is not valid.

### Note
`check_spf` only checks for the sender's identity, not the `helo` value.

### Example
```js
#{
    mail: [
       rule "check spf" || check_spf("spf", "soft")
    ]
}

#{
    mail: [
        // if this check succeed, it wil return `next`.
        // if it fails, it might return `deny` with a custom code
        // (X.7.24 or X.7.25 for example)
        //
        // if you want to use the return status, just put the check_spf
        // function on the last line of your rule.
        rule "check spf 1" || {
            log("debug", `running sender policy framework on ${mail_from()} identity ...`);
            check_spf("spf", "soft")
        },

        // policy is set to "strict" by default.
        rule "check spf 2" || check_spf("both"),
    ],
}
```

</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn check_spf_inner()
```

<details>
<summary markdown="span"> details </summary>

WARNING: This is a low level api.

Get spf record following the Sender Policy Framework (RFC 7208).
see https://datatracker.ietf.org/doc/html/rfc7208

### Return
* a rhai `Map`
    * result (String) : the result of an SPF evaluation.
    * cause  (String) : the "mechanism" that matched or the "problem" error (RFC 7208-9.1).

### Effective smtp stage
`rcpt` and onwards.

### Note
`check_spf` only checks for the sender's identity, not the `helo` value.

### Example
```js
#{
    mail: [
        rule "raw check spf" || {
            let query = check_spf_inner();

            log("debug", `result: ${query.result}`);

            // the 'result' parameter gives you the result of evaluation.
            // (see https://datatracker.ietf.org/doc/html/rfc7208#section-2.6)
            switch query.result {
                "pass" => next(),
                "fail" => {
                    // the 'cause' parameter gives you the cause of the result if there
                    // was an error, and the mechanism of the result if it succeeded.
                    log("error", `check spf error: ${query.cause}`);
                    deny()
                },
                _ => next(),
            };
        },
    ],
}
```

</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn client_address()
```

<details>
<summary markdown="span"> details </summary>

Get the address of the client.

### Effective smtp stage

All of them.

### Return

* `string` - the client's address with the `ip:port` format.

### Example
```js
#{
    connect: [
       action "log info" || log("info", `${client_address()}`),
    ]
}
```

</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn client_ip()
```

<details>
<summary markdown="span"> details </summary>

Get the ip address of the client.

### Effective smtp stage

All of them.

### Return

* `string` - the client's ip address.

### Example
```js
#{
    connect: [
       action "log info" || log("info", `${client_ip()}`),
    ]
}
```

</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn client_port()
```

<details>
<summary markdown="span"> details </summary>

Get the ip port of the client.

### Effective smtp stage

All of them.

### Return

* `int` - the client's port.

### Example
```js
#{
    connect: [
       action "log info" || log("info", `${client_port()}`),
    ]
}
```

</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn connection_timestamp()
```

<details>
<summary markdown="span"> details </summary>

Get a the timestamp of the client's connection time.

### Effective smtp stage

All of them.

### Return

* `timestamp` - the connexion timestamp of the client.

### Example
```js
#{
    connect: [
       action "log info" || log("info", `${connection_timestamp()}`),
    ]
}
```

</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn count_header(header: ?)
```

<details>
<summary markdown="span"> details </summary>

Count the number of headers with the given name.

# Args

* `header` - the name of the header to count.

# Return

* `number` - the number headers with the same name.

# Effective smtp stage

All of them, although it is most useful in the `preq` stage because this
is when the email body is received.

# Example
```js
#{
    postq: [
        action "display VSMTP header" || {
            print(get_header("X-VSMTP"));
        }
    ],
}
```

</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn ctx()
```

<details>
<summary markdown="span"> details </summary>

WARNING: This is a low level function.
Get access to the email context.

### Note
This is used internally to provide encapsulation of vsl's features.
You should not use this function.

### Return

* `the context`

### Effective smtp stage
all of them.

### Example
```js
#{
    connect: [
       action "client ip" || log("info", `client: {client_ip()}`),
    ]
}
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn date()
```

<details>
<summary markdown="span"> details </summary>

Get the current date.

### Return

* `string` - the current date.

### Effective smtp stage

All of them.

### Example
```js
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


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn deliver(rcpt: ?)
```

<details>
<summary markdown="span"> details </summary>

Set the delivery method to deliver for a single recipient.
After all rules are evaluated, the email will be sent
to the recipient using the domain of its address.

### Args

* `rcpt` - the recipient to apply the method to.

### Effective smtp stage

All of them.

### Example
```js
#{
    delivery: [
       action "setup delivery" || deliver("john.doe@example.com"),
    ]
}
```

</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn deliver_all()
```

<details>
<summary markdown="span"> details </summary>

Set the delivery method to deliver for all recipients.
After all rules are evaluated, the email will be sent
to all recipients using the domain of their respective address.

### Effective smtp stage

All of them.

### Example
```js
#{
    delivery: [
       action "setup delivery" || deliver_all(),
    ]
}
```

</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn deny()
```

<details>
<summary markdown="span"> details </summary>

Stop rules evaluation and/or send an error code to the client.
The code sent is `554 - permanent problems with the remote server`.

### Effective smtp stage

all of them.

### Example
```js
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
fn deny(code: ?)
```

<details>
<summary markdown="span"> details </summary>

Stop rules evaluation and/or send a custom code to the client.

### Effective smtp stage

all of them.

### Example
```js
#{
    rcpt: [
        rule "check for satan" || {
           // a custom error code can be used with `deny`.
           const error_code = code(550, "satan.org is not welcome here.");

           // The client is denied if a recipient's domain matches satan.org,
           // this is a blacklist, sort-of.
           if rcpt().domain == "satan.org" {
               deny(error_code)
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
fn dump(dir: ?)
```

<details>
<summary markdown="span"> details </summary>

Export the current message and the envelop to a file as a `json` file.
The message id of the email is used to name the file.

### Args

* `dir` - the directory where to store the data. Relative to the
application path.

### Effective smtp stage

`preq` and onwards.

### Example
```js
#{
    preq: [
       action "dump email" || dump("metadata"),
    ]
}
```

</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn faccept()
```

<details>
<summary markdown="span"> details </summary>

Tell the rule engine to force accept the incoming transaction.
This means that all rules following the one `faccept` is called
will be ignored.

Use this return status when you are sure that
the incoming client can be trusted.

### Effective smtp stage

all of them.

### Example
```js
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

### Module:Status
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn forward(rcpt: ?, target: ?)
```

<details>
<summary markdown="span"> details </summary>

Set the delivery method to forwarding for a single recipient.
After all rules are evaluated, forwarding will be used to deliver
the email to the recipient.

### Args

* `rcpt` - the recipient to apply the method to.
* `target` - the target to forward the email to.

### Effective smtp stage

All of them.

### Example
```js
#{
    delivery: [
       action "setup forwarding" || forward("john.doe@example.com", "mta-john.example.com"),
    ]
}
```

</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn forward_all(target: ?)
```

<details>
<summary markdown="span"> details </summary>

Set the delivery method to forwarding for all recipients.
After all rules are evaluated, forwarding will be used to deliver
the email.

### Args

* `target` - the target to forward the email to.

### Effective smtp stage

All of them.

### Example
```js
#{
    delivery: [
       action "setup forwarding" || forward_all("mta-john.example.com"),
    ]
}
```

</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn get_all_headers()
```

<details>
<summary markdown="span"> details </summary>

Get a list of all headers.

# Return

* `array` - all of the headers found in the message.

# Effective smtp stage

All of them, although it is most useful in the `preq` stage because this
is when the email body is received.

# Example
```js
#{
    postq: [
        action "log display headers" || {
            log("trace", `${get_all_headers()}`);
        }
    ],
}
```

</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn get_all_headers(header: ?)
```

<details>
<summary markdown="span"> details </summary>

Get a list of all values of a specific header from the incoming message.

# Args

* `header` - the name of the header to search.

# Return

* `array` - all header values, or an empty array if the header was not found.

# Effective smtp stage

All of them, although it is most useful in the `preq` stage because this
is when the email body is received.

# Example
```js
#{
    postq: [
        action "display return path" || {
            print(get_all_headers("Return-Path"));
        }
    ],
}
```

</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn get_domain()
```

<details>
<summary markdown="span"> details </summary>

Get the domain of an email address.

### Args

* `address` - the address to extract the domain from.

### Effective smtp stage

All of them.

### Example
```js
#{
    mail: [
        // You can also use the `get_domain(mail_from())` syntax.
        action "display sender's domain" || {
            log("info", `received a message from domain ${mail_from().domain}.`);
        }
    ],
}
```

</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn get_domains()
```

<details>
<summary markdown="span"> details </summary>

Get all domains of the recipient list.

### Args

* `rcpt_list` - the recipient list.

### Effective smtp stage

`mail` and onwards.

### Example
```js
#{
    mail: [
        action "display recipients domains" || {
            print("list of recipients domains:");

            // You can also use the `get_domains(rcpt_list())` syntax.
            for domain in rcpt_list().domains {
                print(`- ${domain}`);
            }
        }
    ],
}
```

</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn get_header(header: ?)
```

<details>
<summary markdown="span"> details </summary>

Get a specific header from the incoming message.

### Args

* `header` - the name of the header to get.

### Return

* `string` - the header value, or an empty string if the header was not found.

### Effective smtp stage

All of them, although it is most useful in the `preq` stage because this
is when the email body is received.

### Example
```js
#{
    postq: [
        action "display VSMTP header" || {
            print(get_header("X-VSMTP"));
        }
    ],
}
```

</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn get_local_part()
```

<details>
<summary markdown="span"> details </summary>

Get the local part of an email address.

### Args

* `address` - the address to extract the local part from.

### Effective smtp stage

All of them.

### Example
```js
#{
    mail: [
        // You can also use the `get_local_part(mail_from())` syntax.
        action "display mail from identity" || {
            log("info", `received a message from ${mail_from().local_part}.`);
        }
    ],
}
```

</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn get_local_parts()
```

<details>
<summary markdown="span"> details </summary>

Get all local parts of the recipient list.

### Args

* `rcpt_list` - the recipient list.

### Effective smtp stage

`mail` and onwards.

### Example
```js
#{
    mail: [
        action "display recipients usernames" || {
            print("list of recipients user names:");

            // You can also use the `get_local_parts(rcpt_list())` syntax.
            for user in rcpt_list().local_parts {
                print(`- ${user}`);
            }
        }
    ],
}
```

</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn has_header(header: ?)
```

<details>
<summary markdown="span"> details </summary>

Checks if the message contains a specific header.

### Args

* `header` - the name of the header to search.

### Effective smtp stage

All of them, although it is most useful in the `preq` stage because this
is when the email body is received.

### Example
```js
#{
    postq: [
        action "check for VSMTP header" || {
            if has_header("X-VSMTP") {
                log("info", "incoming message could be from another vsmtp server");
            }
        }
    ],
}
```

</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn helo()
```

<details>
<summary markdown="span"> details </summary>

Get the value of the `HELO/EHLO` command sent by the client.

### Effective smtp stage

`helo` and onwards.

### Return

* `string` - the value of the `HELO/EHLO` command.

### Example
```js
#{
    helo: [
       action "log info" || log("info", `${helo()}`),
    ]
}
```

</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn hostname()
```

<details>
<summary markdown="span"> details </summary>

Get the hostname of this machine.

### Return

* `string` - the host name of the machine.

### Effective smtp stage

All of them.

### Example
```js
#{
    preq: [
       action "append info header" || {
            append_header("X-VSMTP", `email received by ${hostname()}.`);
       }
    ]
}
```

</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn info(code: ?)
```

<details>
<summary markdown="span"> details </summary>

Ask the client to retry to send the current command by sending an information code.

### Effective smtp stage

all of them.

### Example
```js
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
fn is_authenticated()
```

<details>
<summary markdown="span"> details </summary>

Check if the client is authenticated.

### Effective smtp stage

`authenticate` only.

### Return

* `bool` - true if the client succeeded to authenticate itself, false otherwise.

### Example
```js
#{
    authenticate: [
       action "log info" || log("info", `${is_authenticated()}`),
    ]
}
```

</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn is_secured()
```

<details>
<summary markdown="span"> details </summary>

Has the connection been secured under the encryption protocol SSL/TLS

### Effective smtp stage

all

### Return

* boolean value (`true` if the connection is secured, `false` otherwise)

### Example
```js
#{
  mail: [
    action "log ssl/tls" || {
      log("info", `My client is ${if is_secured() { "secured" } else { "unsecured!!!" }}`)
    }
  ]
}
```

</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn log(level: ?, message: ?)
```

<details>
<summary markdown="span"> details </summary>

Log information to stdout in `nodaemon` mode or to a file.

### Args

* `level` - the level of the message, can be "trace", "debug", "info", "warn" or "error".
* `message` - the message to log.

### Effective smtp stage

All of them.

### Example
```js
#{
    preq: [
       action "log info" || log("info", "this is an informational log."),
    ]
}
```

</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn lookup(host: ?)
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

### Example
```js
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

</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn mail()
```

<details>
<summary markdown="span"> details </summary>

Get a copy of the whole email as a string.

### Effective smtp stage

`preq` and onwards.

### Example
```js
#{
    postq: [
       action "display email content" || log("trace", `email content: ${mail()}`),
    ]
}
```

</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn mail_from()
```

<details>
<summary markdown="span"> details </summary>

Get the value of the `MAIL FROM` command sent by the client.

### Effective smtp stage

`mail` and onwards.

### Return

* `address` - the sender address.

### Example
```js
#{
    helo: [
       action "log info" || log("info", `${mail_from()}`),
    ]
}
```

</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn mail_timestamp()
```

<details>
<summary markdown="span"> details </summary>

Get the time of reception of the email.

### Effective smtp stage

`preq` and onwards.

### Return

* `string` - the timestamp.

### Example
```js
#{
    preq: [
       action "receiving the email" || log("info", `time of reception: ${mail_timestamp()}`),
    ]
}
```

</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn maildir(rcpt: ?)
```

<details>
<summary markdown="span"> details </summary>

Set the delivery method to maildir for a recipient.
After all rules are evaluated, the email will be stored
locally in the `~/Maildir/new/` folder of the recipient's user if it exists on the server.

### Args

* `rcpt` - the recipient to apply the method to.

### Effective smtp stage

All of them.

### Example
```js
#{
    delivery: [
       action "setup maildir" || maildir("john.doe@example.com"),
    ]
}
```

</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn maildir_all()
```

<details>
<summary markdown="span"> details </summary>

Set the delivery method to maildir for all recipients.
After all rules are evaluated, the email will be stored
locally in each `~/Maildir/new` folder of they respective recipient
if they exists on the server.

### Effective smtp stage

All of them.

### Example
```js
#{
    delivery: [
       action "setup mbox" || mbox_all(),
    ]
}
```

</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn mbox(rcpt: ?)
```

<details>
<summary markdown="span"> details </summary>

Set the delivery method to mbox for a recipient.
After all rules are evaluated, the email will be stored
locally in the mail box of the recipient if it exists on the server.

### Args

* `rcpt` - the recipient to apply the method to.

### Effective smtp stage

All of them.

### Example
```js
#{
    delivery: [
       action "setup mbox" || mbox("john.doe@example.com"),
    ]
}
```

</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn mbox_all()
```

<details>
<summary markdown="span"> details </summary>

Set the delivery method to mbox for all recipients.
After all rules are evaluated, the email will be stored
locally in the mail box of all recipients if they exists on the server.

### Effective smtp stage

All of them.

### Example
```js
#{
    delivery: [
       action "setup mbox" || mbox_all(),
    ]
}
```

</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn message_id()
```

<details>
<summary markdown="span"> details </summary>

Get the unique id of the received message.

### Effective smtp stage

`preq` and onwards.

### Return

* `string` - the message id.

### Example
```js
#{
    preq: [
       action "message received" || log("info", `message id: ${message_id()}`),
    ]
}
```

</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn msg()
```

<details>
<summary markdown="span"> details </summary>

WARNING: This is a low level function.
Get access to the message.

### Note
This is used internally to provide encapsulation of vsl's features.
You should not use this function.

### Return

* `the message`

### Effective smtp stage
all of them.

### Example
```js
#{
    connect: [
       action "raw message" || msg().rewrite_mail_from_message("john.doe@example.com"),
    ]
}
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn next()
```

<details>
<summary markdown="span"> details </summary>

Tell the rule engine that a rule succeeded.

### Effective smtp stage

all of them.

### Example
```js
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
fn prepend_header(header: ?, value: ?)
```

<details>
<summary markdown="span"> details </summary>

Add a new header on top all other headers in the message.

### Args

* `header` - the name of the header to prepend.
* `value` - the value of the header to prepend.

### Effective smtp stage

All of them. Even though the email is not received at the current stage,
vsmtp stores new headers and will add them on top of the ones received once
the `preq` stage is reached.

### Example
```js
#{
    postq: [
        action "prepend a header" || {
            prepend_header("X-JOHN", "received by john's server.");
        }
    ],
}
```

</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn quarantine(queue: ?)
```

<details>
<summary markdown="span"> details </summary>

Skip all rules until the email is received and place the email in a
quarantine queue.

### Args

* `queue` - the relative path to the queue where the email will be quarantined. This path will be concatenated to the [app.dirpath] field in your `vsmtp.toml`.

### Effective smtp stage

all of them.

### Example
```js
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


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn rcpt()
```

<details>
<summary markdown="span"> details </summary>

Get the value of the current `RCPT TO` command sent by the client.

### Effective smtp stage

`rcpt` and onwards. Please note that `rcpt()` will always return
the last recipient received in stages after the `rcpt` stage. Therefore,
this functions is best used in the `rcpt` stage.

### Return

* `address` - the address of the received recipient.

### Example
```js
#{
    rcpt: [
       action "log recipients" || log("info", `new recipient: ${rcpt()}`),
    ]
}
```

</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn rcpt_list()
```

<details>
<summary markdown="span"> details </summary>

Get the list of recipients received by the client.

### Effective smtp stage

`rcpt` and onwards. Note that you will not have all recipients received
all at once in the `rcpt` stage. It is better to use this function
in the later stages.

### Return

* `Array of addresses` - the list containing all recipients.

### Example
```js
#{
    preq: [
       action "log recipients" || log("info", `all recipients: ${rcpt_list()}`),
    ]
}
```

</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn remove_header(header: ?)
```

<details>
<summary markdown="span"> details </summary>

Remove an existing header from the message.

# Args

* `header` - the name of the header to remove.

# Return

* a boolean value, true if a header has been removed, false otherwise.

# Effective smtp stage

All of them, although it is most useful in the `preq` stage because this
is when the email body is received.

# Example
```js
#{
    postq: [
        action "remove one X-VSMTP header" || {
            remove_header("X-VSMTP");
        },

        // There can be multiple headers with the same name.
        // Since `remove_header` return `true` when it removes an
        // header, you can use a `while` loop to remove all headers
        // that bear the same name.
        action "remove all X-VSMTP headers" || {
            while remove_header("X-VSMTP") is true {}
        },
    ],
}
```

</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn remove_rcpt_envelop(rcpt: ?)
```

<details>
<summary markdown="span"> details </summary>

Remove a recipient from the envelop. Note that this does not remove
the recipient from the `To` header. Use `remove_rcpt_message` for that.

### Args

* `rcpt` - the recipient to remove.

### Effective smtp stage

All of them.

### Example
```js
#{
    preq: [
       // never deliver to "john.doe@example.com".
       action "rewrite envelop" || remove_rcpt_envelop("john.doe@example.com"),
    ]
}
```

</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn remove_rcpt_message(addr: ?)
```

<details>
<summary markdown="span"> details </summary>

Remove a recipient from the `To` header of the message.

### Args

* `addr` - the recipient to remove to the `To` header.

### Effective smtp stage

`preq` and onwards.

### Example
```js
#{
    preq: [
       action "update recipients" || remove_rcpt_message("john.doe@example.com"),
    ]
}
```

</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn rename_header(o: ?, n: ?)
```

<details>
<summary markdown="span"> details </summary>

Replace an existing header name by a new value.

# Args

* `old` - the name of the header to rename.
* `new` - the new new of the header.

# Effective smtp stage

All of them, although it is most useful in the `preq` stage because this
is when the email body is received.

# Example
```js
#{
    postq: [
        action "rename header" || {
            rename_header("X-To-Rename", "X-Renamed");
        }
    ],
}
```

</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn rewrite_mail_from(new_addr: ?)
```

<details>
<summary markdown="span"> details </summary>

Rewrite the value of the `MAIL FROM` command has well has
the `From` header.

### Args

* `new_addr` - the new sender address to set.

### Effective smtp stage

`preq` and onwards.

### Example
```js
#{
    preq: [
       action "rewrite sender" || rewrite_mail_from("john.doe@example.com"),
    ]
}
```

</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn rewrite_mail_from_envelop(new_addr: ?)
```

<details>
<summary markdown="span"> details </summary>

Rewrite the sender received from the `MAIL FROM` command.

### Args

* `new_addr` - the new sender address to set.

### Effective smtp stage

`mail` and onwards.

### Example
```js
#{
    preq: [
       action "rewrite envelop" || rewrite_mail_from_envelop("unknown@example.com"),
    ]
}
```

</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn rewrite_mail_from_message(new_addr: ?)
```

<details>
<summary markdown="span"> details </summary>

Change the sender's address in the `From` header of the message.

### Args

* `new_addr` - the new sender address to set.

### Effective smtp stage

`preq` and onwards.

### Example
```js
#{
    preq: [
       action "replace sender" || rewrite_mail_from_message("john.server@example.com"),
    ]
}
```

</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn rewrite_rcpt_envelop(old_addr: ?, new_addr: ?)
```

<details>
<summary markdown="span"> details </summary>

Replace a recipient received by a `RCPT TO` command.

### Args

* `old_addr` - the recipient to replace.
* `new_addr` - the new address to use when replacing `old_addr`.

### Effective smtp stage

`rcpt` and onwards.

### Example
```js
#{
    preq: [
       action "rewrite envelop" || rewrite_rcpt_envelop("john.doe@example.com", "john.main@example.com"),
    ]
}
```

</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn rewrite_rcpt_message(old_addr: ?, new_addr: ?)
```

<details>
<summary markdown="span"> details </summary>

Replace a recipient by an other in the `To` header of the message.

### Args

* `old_addr` - the recipient to replace.
* `new_addr` - the new address to use when replacing `old_addr`.

### Effective smtp stage

`preq` and onwards.

### Example
```js
#{
    preq: [
       action "rewrite recipient" || rewrite_rcpt_message("john.doe@example.com", "john-mta@example.com"),
    ]
}
```

</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn rlookup(ip: ?)
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

### Example
```js
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

</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn server_address()
```

<details>
<summary markdown="span"> details </summary>

Get the full server address.

### Effective smtp stage

All of them.

### Return

* `string` - the server's address with the `ip:port` format.

### Example
```js
#{
    connect: [
       action "log info" || log("info", `${server_address()}`),
    ]
}
```

</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn server_ip()
```

<details>
<summary markdown="span"> details </summary>

Get the server's ip.

### Effective smtp stage

All of them.

### Return

* `string` - the server's ip.

### Example
```js
#{
    connect: [
       action "log info" || log("info", `${server_ip()}`),
    ]
}
```

</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn server_name()
```

<details>
<summary markdown="span"> details </summary>

Get the name of the server.

### Effective smtp stage

All of them.

### Return

* `string` - the name of the server.

### Example
```js
#{
    connect: [
       action "log info" || log("info", `${server_name()}`),
    ]
}
```

</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn server_port()
```

<details>
<summary markdown="span"> details </summary>

Get the server's port.

### Effective smtp stage

All of them.

### Return

* `string` - the server's port.

### Example
```js
#{
    connect: [
       action "log info" || log("info", `${server_port()}`),
    ]
}
```

</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn set_header(header: ?, value: ?)
```

<details>
<summary markdown="span"> details </summary>

Replace an existing header value by a new value, or append a new header
to the message.

### Args

* `header` - the name of the header to set or add.
* `value` - the value of the header to set or add.

### Effective smtp stage

All of them. Even though the email is not received at the current stage,
vsmtp stores new headers and will add them on top to the ones received once
the `preq` stage is reached.

Be aware that if you want to set a header value from the original message,
you must use `set_header` in the `preq` stage and onwards.

### Example
```js
#{
    postq: [
        action "update subject" || {
            let subject = get_header("Subject");
            set_header("Subject", `${subject} (analyzed by vsmtp)`);
        }
    ],
}
```

</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn sign_dkim(selector: ?, private_key: ?)
```

<details>
<summary markdown="span"> details </summary>

Syntactic sugar for:
```
sign_dkim(
  selector,
  private_key,
  ["From", "To", "Date", "Subject", "From"],
  "simple/relaxed"
)
```

### Module:Security
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn sign_dkim(selector: ?, private_key: ?, headers_field: ?, canonicalization: ?)
```

<details>
<summary markdown="span"> details </summary>

Produce a `DKIM-Signature` header.

### Args

* `selector` - the DNS selector to expose the public key & for the verifier
* `private_key` - the private key to sign the mail,
    associated with the public key in the `selector._domainkey.sdid` DNS record
* `headers_field` - list of headers to sign
* `canonicalization` - the canonicalization algorithm to use (ex: "simple/relaxed")

### Effective smtp stage

`preq` and onwards.

### Example

```js
#{
  preq: [
    action "sign dkim" || {
      sign_dkim("2022-09", ["From", "To", "Date", "Subject", "From"], "simple/relaxed");
    },
  ]
}
```

</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn srv()
```

<details>
<summary markdown="span"> details </summary>

WARNING: This is a low level function.
Get access to the server context.

### Note
This is used internally to provide encapsulation of vsl's features.
You should not use this function.

### Return

* `the server api`

### Effective smtp stage
all of them.

### Example
```js
#{
    connect: [
       action "raw lookup" || srv().lookup("example.com"),
    ]
}
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn time()
```

<details>
<summary markdown="span"> details </summary>

Get the current time.

### Return

* `string` - the current time.

### Effective smtp stage

All of them.

### Example
```js
#{
    preq: [
       action "append info header" || {
            append_header("X-VSMTP", `email received by ${hostname()} the ${date()} at ${time()}.`);
       }
    ]
}
```

</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn user_exist(name: ?)
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

### Example
```js
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

</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn verify_dkim()
```

<details>
<summary markdown="span"> details </summary>

Verify the `DKIM-Signature` header(s) in the mail and produce a `Authentication-Results`.
If this function has already been called once, it will return the result of the previous call.
see https://datatracker.ietf.org/doc/html/rfc6376

### Return

* a DkimResult object

### Effective smtp stage

`preq` and onwards.

### Example

```js
#{
  preq: [
    action "check dkim" || { verify_dkim(); },
  ]
}
````

### Module:Security
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn verify_dkim_inner(policy: ?)
```

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn write(dir: ?)
```

<details>
<summary markdown="span"> details </summary>

Export the current raw message to a file as an `eml` file.
The message id of the email is used to name the file.

### Args

* `dir` - the directory where to store the email. Relative to the
application path.

### Effective smtp stage

`preq` and onwards.

### Example
```js
#{
    preq: [
       action "write to file" || write("archives"),
    ]
}
```

</details>

</div>
</br>

