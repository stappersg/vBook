# global



<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn !=(this: SharedObject, s: String) -> bool
```

<details>
<summary markdown="span"> details </summary>

Operator `!=` for `SharedObject` and `&str`
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn !=(this: SharedObject, other: SharedObject) -> bool
```

<details>
<summary markdown="span"> details </summary>

Operator `!=` for `SharedObject`
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn !=(this: String, other: SharedObject) -> bool
```

<details>
<summary markdown="span"> details </summary>

Operator `!=` for `&str` and `SharedObject`
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn !=(in1: Status, in2: Status) -> bool
```

<details>
<summary markdown="span"> details </summary>

Operator `!=` for `Status`
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn ==(this: SharedObject, s: String) -> bool
```

<details>
<summary markdown="span"> details </summary>

Operator `==` for `SharedObject` and `&str`
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn ==(this: String, other: SharedObject) -> bool
```

<details>
<summary markdown="span"> details </summary>

Operator `==` for `&str` and `SharedObject`
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn ==(this: SharedObject, other: SharedObject) -> bool
```

<details>
<summary markdown="span"> details </summary>

Operator `==` for `SharedObject`
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn ==(in1: Status, in2: Status) -> bool
```

<details>
<summary markdown="span"> details </summary>

Operator `==` for `Status`
</details>

</div>
</br>


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
fn add_rcpt_envelop(context: Context, new_addr: String) -> ()
```

<details>
<summary markdown="span"> details </summary>

Add a new recipient to the envelop. Note that this does not add
the recipient to the `To` header. Use `add_rcpt_message` for that.

# Args

* `rcpt` - the new recipient to add.

# Effective smtp stage

All of them.

# Examples

```
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
fn add_rcpt_envelop(context: Context, new_addr: SharedObject) -> ()
```

<details>
<summary markdown="span"> details </summary>

Add a new recipient to the envelop. Note that this does not add
the recipient to the `To` header. Use `add_rcpt_message` for that.

# Args

* `rcpt` - the new recipient to add.

# Effective smtp stage

All of them.

# Examples

```
#{
    connect: [
       // always deliver a copy of the message to "john.doe@example.com".
       action "rewrite envelop" || add_rcpt_envelop(address("john.doe@example.com")),
    ]
}
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn add_rcpt_message(message: Message, new_addr: String) -> ()
```

<details>
<summary markdown="span"> details </summary>

Add a recipient to the `To` header of the message.

# Args

* `addr` - the recipient address to add to the `To` header.

# Effective smtp stage

`preq` and onwards.

# Examples

```
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
fn add_rcpt_message(message: Message, new_addr: SharedObject) -> ()
```

<details>
<summary markdown="span"> details </summary>

Add a recipient to the `To` header of the message.

# Args

* `addr` - the recipient address to add to the `To` header.

# Effective smtp stage

`preq` and onwards.

# Examples

```
#{
    preq: [
       action "update recipients" || add_rcpt_message(address("john.doe@example.com")),
    ]
}
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn address(address: String) -> VSLObject
```

<details>
<summary markdown="span"> details </summary>

an email address (jones@foo.com)
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn append_header(message: Message, header: String, value: SharedObject) -> ()
```

<details>
<summary markdown="span"> details </summary>

Add a new header **at the end** of the header list in the message.

# Args

* `header` - the name of the header to append.
* `value` - the value of the header to append.

# Effective smtp stage

All of them. Even though the email is not received at the current stage,
vsmtp stores new headers and will add them on top of the ones received once
the `preq` stage is reached.

# Examples

```
#{
    postq: [
        action "append a header" || {
            append_header("X-JOHN", "received by john's server.");
        }
    ],
}
```

```
"X-My-Header: 250 foo\r\n",
"Subject: Unit test are cool\r\n",
"\r\n",
"Hello world!\r\n",

#{
  preq: [
    rule "append_header" || {
      append_header("X-My-Header-2", "bar");
      append_header("X-My-Header-3", identifier("baz"));
    }
  ]
}
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn append_header(message: Message, header: String, value: String) -> ()
```

<details>
<summary markdown="span"> details </summary>

Add a new header **at the end** of the header list in the message.

# Args

* `header` - the name of the header to append.
* `value` - the value of the header to append.

# Effective smtp stage

All of them. Even though the email is not received at the current stage,
vsmtp stores new headers and will add them on top of the ones received once
the `preq` stage is reached.

# Examples

```
#{
    postq: [
        action "append a header" || {
            append_header("X-JOHN", "received by john's server.");
        }
    ],
}
```

```
"X-My-Header: 250 foo\r\n",
"Subject: Unit test are cool\r\n",
"\r\n",
"Hello world!\r\n",

#{
  preq: [
    rule "append_header" || {
      append_header("X-My-Header-2", "bar");
      append_header("X-My-Header-3", identifier("baz"));
    }
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

# Args

* `rcpt` - the recipient to add as a blind carbon copy.

# Effective smtp stage

All of them.

# Examples

```rust
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

# Effective smtp stage

`preq` and onwards.

# Example

```
#{
  preq: [
    rule "check dmarc" || { check_dmarc() },
  ]
}
```

# Module:Security
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

# Args

* `header` - "spf" | "auth" | "both" | "none"

# Return
* `deny(code550_7_23 | code451_7_24 | code550_7_24)` - an error occurred during lookup. (returned even when a softfail is received using the "strict" policy)
* `next()` - the operation succeeded.

# Effective smtp stage
`rcpt` and onwards.

# Errors
* The `header` argument is not valid.
* The `policy` argument is not valid.

# Note
`check_spf` only checks for the sender's identity, not the `helo` value.

# Example
```
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
# Module:Security
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

# Args

* `header` - "spf" | "auth" | "both" | "none"
* `policy` - "strict" | "soft"

# Return
* `deny(code550_7_23 | code451_7_24 | code550_7_24)` - an error occurred during lookup. (returned even when a softfail is received using the "strict" policy)
* `next()` - the operation succeeded.

# Effective smtp stage
`rcpt` and onwards.

# Errors
* The `header` argument is not valid.
* The `policy` argument is not valid.

# Note
`check_spf` only checks for the sender's identity, not the `helo` value.

# Example
```
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

# Module:Security
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn check_spf(ctx: Context, srv: Server) -> Map
```

<details>
<summary markdown="span"> details </summary>

evaluate a sender identity.
the identity parameter can be 'helo', 'mail_from' or 'both'.

# Results
a rhai Map with:
   * result (String) : the result of an SPF evaluation.
   * cause  (String) : the "mechanism" that matched or the "problem" error (RFC 7208-9.1).
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

# Return
* a rhai `Map`
    * result (String) : the result of an SPF evaluation.
    * cause  (String) : the "mechanism" that matched or the "problem" error (RFC 7208-9.1).

# Effective smtp stage
`rcpt` and onwards.

# Note
`check_spf` only checks for the sender's identity, not the `helo` value.

# Example
```
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

# Module:Security
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn cmd(parameters: Map) -> Cmd
```

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn code(code: int, text: String) -> VSLObject
```

<details>
<summary markdown="span"> details </summary>

A SMTP code with the code and message as parameter.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn code(code: int, enhanced: String, text: String) -> VSLObject
```

<details>
<summary markdown="span"> details </summary>

A SMTP code with the code and message as parameter and an enhanced code.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn contains(this: SharedObject, other: SharedObject) -> bool
```

<details>
<summary markdown="span"> details </summary>

Operator `contains`
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn contains(map: Map, object: SharedObject) -> bool
```

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn contains(this: SharedObject, s: String) -> bool
```

<details>
<summary markdown="span"> details </summary>

Operator `contains`
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn count_header(message: Message, header: String) -> int
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

# Examples

```
#{
    postq: [
        action "display VSMTP header" || {
            print(get_header("X-VSMTP"));
        }
    ],
}
```

```
"X-My-Header: foo\r\n",
"X-My-Header: bar\r\n",
"X-My-Header: baz\r\n",
"Subject: Unit test are cool\r\n",
"\r\n",
"Hello world!\r\n",

#{
  preq: [
    rule "count_header" || {
      accept(`250 count is ${count_header("X-My-Header")} and ${count_header(identifier("Subject"))}`);
    }
  ]
}
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn count_header(message: Message, header: SharedObject) -> int
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

# Examples

```
#{
    postq: [
        action "display VSMTP header" || {
            print(get_header(identifier("X-VSMTP")));
        }
    ],
}
```

```
"X-My-Header: foo\r\n",
"X-My-Header: bar\r\n",
"X-My-Header: baz\r\n",
"Subject: Unit test are cool\r\n",
"\r\n",
"Hello world!\r\n",

#{
  preq: [
    rule "count_header" || {
      accept(`250 count is ${count_header("X-My-Header")} and ${count_header(identifier("Subject"))}`);
    }
  ]
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

# Note
This is used internally to provide encapsulation of vsl's features.
You should not use this function directly.

# Return

* `the context`

# Effective smtp stage

all of them.

# Examples

```rust
#{
    connect: [
       action "client ip" || log("info", `client: {ctx().client_ip}`),
    ]
}
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
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
fn deliver(context: Context, rcpt: String) -> ()
```

<details>
<summary markdown="span"> details </summary>

Set the delivery method to deliver for a single recipient.
After all rules are evaluated, the email will be sent
to the recipient using the domain of its address.

# Args

* `rcpt` - the recipient to apply the method to.

# Effective smtp stage

All of them.

# Examples
```
#{
    delivery: [
       action "setup delivery" || deliver("john.doe@example.com"),
    ]
}
```

```
 #{
   rcpt: [
     action "deliver (str/str)" || {
       add_rcpt_envelop("my.address@foo.com");
       deliver("my.address@foo.com");
     },
     action "deliver (obj/str)" || {
       let rcpt = address("my.address@bar.com");
       add_rcpt_envelop(rcpt);
       deliver(rcpt);
     },
     action "deliver (str/obj)" || {
       let target = ip6("::1");
       add_rcpt_envelop("my.address@baz.com");
       deliver("my.address@baz.com");
     },
     action "deliver (obj/obj)" || {
       let rcpt = address("my.address@boz.com");
       add_rcpt_envelop(rcpt);
       deliver(rcpt);
     },
   ],
 }

```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn deliver(context: Context, rcpt: SharedObject) -> ()
```

<details>
<summary markdown="span"> details </summary>

Set the delivery method to deliver for a single recipient.
After all rules are evaluated, the email will be sent
to the recipient using the domain of its address.

# Args

* `rcpt` - the recipient to apply the method to.

# Effective smtp stage

All of them.

# Example
```
#{
    delivery: [
       action "setup delivery" || deliver(address("john.doe@example.com")),
    ]
}
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn deliver_all(context: Context) -> ()
```

<details>
<summary markdown="span"> details </summary>

Set the delivery method to deliver for all recipients.
After all rules are evaluated, the email will be sent
to all recipients using the domain of their respective address.

# Effective smtp stage

All of them.

# Examples

```
#{
    delivery: [
       action "setup delivery" || deliver_all(),
    ]
}
```

```
 #{
   rcpt: [
     action "deliver_all" || {
       add_rcpt_envelop("my.address@foo.com");
       add_rcpt_envelop("my.address@bar.com");
       deliver_all();
     },
   ],
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
fn dmarc_check(record: Record, rfc5322_from: String, dkim_result: Map, spf_mail_from: String, spf_result: String) -> bool
```

<details>
<summary markdown="span"> details </summary>


</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn dump(srv: Server, mut ctx: Context, dir: String) -> ()
```

<details>
<summary markdown="span"> details </summary>

write the content of the current email with it's metadata in a json file.
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
fn file(path: String, content_type: String) -> Array
```

<details>
<summary markdown="span"> details </summary>

the content of a file.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn forward(context: Context, rcpt: SharedObject, forward: String) -> ()
```

<details>
<summary markdown="span"> details </summary>

Set the delivery method to forwarding for a single recipient.
After all rules are evaluated, forwarding will be used to deliver
the email to the recipient.

# Args

* `rcpt` - the recipient to apply the method to.
* `target` - the target to forward the email to.

# Effective smtp stage

All of them.

# Examples
```
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
fn forward(context: Context, rcpt: String, forward: SharedObject) -> ()
```

<details>
<summary markdown="span"> details </summary>

Set the delivery method to forwarding for a single recipient.
After all rules are evaluated, forwarding will be used to deliver
the email to the recipient.

# Args

* `rcpt` - the recipient to apply the method to.
* `target` - the target to forward the email to.

# Effective smtp stage

All of them.

# Examples
```
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
fn forward(context: Context, rcpt: String, forward: String) -> ()
```

<details>
<summary markdown="span"> details </summary>

Set the delivery method to forwarding for a single recipient.
After all rules are evaluated, forwarding will be used to deliver
the email to the recipient.

# Args

* `rcpt` - the recipient to apply the method to.
* `target` - the target to forward the email to.

# Effective smtp stage

All of them.

# Examples
```
const rules = #{
    delivery: [
       action "setup forwarding" || forward("john.doe@example.com", "mta-john.example.com"),
    ]
}
```

```
#{
    rcpt: [
      action "forward (str/str)" || {
        add_rcpt_envelop("my.address@foo.com");
        forward("my.address@foo.com", "127.0.0.1");
      },
      action "forward (obj/str)" || {
        let rcpt = address("my.address@bar.com");
        add_rcpt_envelop(rcpt);
        forward(rcpt, "127.0.0.2");
      },
      action "forward (str/obj)" || {
        let target = ip6("::1");
        add_rcpt_envelop("my.address@baz.com");
        forward("my.address@baz.com", target);
      },
      action "forward (obj/obj)" || {
        let rcpt = address("my.address@boz.com");
        add_rcpt_envelop(rcpt);
        forward(rcpt, ip4("127.0.0.4"));
      },
    ],
}

```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn forward(context: Context, rcpt: SharedObject, forward: SharedObject) -> ()
```

<details>
<summary markdown="span"> details </summary>

Set the delivery method to forwarding for a single recipient.
After all rules are evaluated, forwarding will be used to deliver
the email to the recipient.

# Args

* `rcpt` - the recipient to apply the method to.
* `target` - the target to forward the email to.

# Effective smtp stage

All of them.

# Examples
```
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
fn forward_all(context: Context, forward: String) -> ()
```

<details>
<summary markdown="span"> details </summary>

Set the delivery method to forwarding for all recipients.
After all rules are evaluated, forwarding will be used to deliver
the email.

# Args

* `target` - the target to forward the email to.

# Effective smtp stage

All of them.

# Examples

```
#{
    delivery: [
       action "setup forwarding" || forward_all("mta-john.example.com"),
    ]
}
```

```
 #{
   rcpt: [
     action "forward_all" || {
       add_rcpt_envelop("my.address@foo.com");
       add_rcpt_envelop("my.address@bar.com");
       forward_all("127.0.0.1");
     },
     action "forward_all (obj)" || {
       add_rcpt_envelop("my.address@foo2.com");
       add_rcpt_envelop("my.address@bar2.com");
       forward_all(ip4("127.0.0.1"));
     },
   ],
 }

```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn forward_all(context: Context, forward: SharedObject) -> ()
```

<details>
<summary markdown="span"> details </summary>

Set the delivery method to forwarding for all recipients.
After all rules are evaluated, forwarding will be used to deliver
the email.

# Args

* `target` - the target to forward the email to.

# Effective smtp stage

All of them.

# Examples

```
#{
    delivery: [
       action "setup forwarding" || forward_all(fqdn("mta-john.example.com")),
    ]
}
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn fqdn(domain: String) -> VSLObject
```

<details>
<summary markdown="span"> details </summary>

a valid fully qualified domain name (foo.com)
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn generate_signature_dkim(message: Message, context: Context, selector: String, private_key: Arc<PrivateKey>, headers_field: Array, canonicalization: String) -> String
```

<details>
<summary markdown="span"> details </summary>

Create a new signature of the message for the DKIM.

# Examples

```
let msg = r#"
Date: Wed, 26 Oct 2022 14:30:51 -0700
From: Mathieu Lala <noreply@github.com>
To: mlala@negabit.com
Subject: Testing and documenting the dkim signature

This message has not been signed yet, meaning someone could change it...
"#;



 #{
   postq: [
     action "add a DKIM signature" || {
       for i in get_private_keys(srv(), "testserver.com") {
         sign_dkim("2022-09", i, ["From", "To", "Date", "Subject", "From"], "simple/relaxed");
       }
     },
     rule "check signature" || {
       let signature = "v=1; a=rsa-sha256; d=testserver.com; s=2022-09;\r\n\
           \tc=simple/relaxed; q=dns/txt; h=From:To:Date:Subject:From;\r\n\
           \tbh=ATHiC1KD8OegIorswWts+SlujGUpgqR6pqXYlNWA01Y=;\r\n\tb=Ur\
           /frdH3beyU3LRQMGBdI6OdxRvfpu+s04hmHcVkpBYzR4cXuDPByWpUCqhO4C\
           sEwpPRDcWQtsCfuzSK1FTf7XCWgsKKGPmsdQ40pUviA0UrrzpIDIziMxSI/S\
           8ohNnxvqxrtxZoN6Wo2lnQ+kYAATYxJPOjC57JIBJ89RGrf+6Wbvz6/PofcU\
           9VwpylegZRU5Cial69lN2qaIkoVFOE9fz8ZIz9VV2A9Lh/xgKFM7eipBWCR6\
           ZUU1HZTbSiqiL9Q6A823az/E2jqOUZXtsGK/Bo/vDjTV166d5vY34JA3189C\
           x83Rbif9A/kdCO6C8gGK0WOasp5R0ONmVz41TaGQ==";

       if get_header("DKIM-Signature") == signature {
         accept()
       } else {
         deny()
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
fn get auid(signature: Signature) -> String
```

<details>
<summary markdown="span"> details </summary>

return the `auid` property of the [`Signature`]
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn get auth(context: Context) -> Credentials
```

<details>
<summary markdown="span"> details </summary>

Get authentication credentials from the client.

# Effective smtp stage

`authenticate` only.

# Return

* `Credentials` - the credentials of the client.

# Example

```
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
fn get authid(credentials: Credentials) -> String
```

<details>
<summary markdown="span"> details </summary>

Get the `authid` property of the connection.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn get authpass(credentials: Credentials) -> String
```

<details>
<summary markdown="span"> details </summary>

Get the `authpass` property of the connection.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn get client_address(context: Context) -> String
```

<details>
<summary markdown="span"> details </summary>

Get the address of the client.

# Effective smtp stage

All of them.

# Return

* `string` - the client's address with the `ip:port` format.

# Example

```
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
fn get client_ip(context: Context) -> String
```

<details>
<summary markdown="span"> details </summary>

Get the ip address of the client.

# Effective smtp stage

All of them.

# Return

* `string` - the client's ip address.

# Example

```
#{
    connect: [
       action "log info" || log("info", `client ip: ${client_ip()}`),
    ]
}
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn get client_port(context: Context) -> int
```

<details>
<summary markdown="span"> details </summary>

Get the ip port of the client.

# Effective smtp stage

All of them.

# Return

* `int` - the client's port.

# Example

```
#{
    connect: [
       action "log info" || log("info", `client port: ${client_port()}`),
    ]
}
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn get connection_timestamp(context: Context) -> OffsetDateTime
```

<details>
<summary markdown="span"> details </summary>

Get a the timestamp of the client's connection time.

# Effective smtp stage

All of them.

# Return

* `timestamp` - the connexion timestamp of the client.

# Example

```
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
fn get dkim_result(ctx: Context) -> Map
```

<details>
<summary markdown="span"> details </summary>

Return the DKIM signature verification result in the `ctx()` or
an error if no result is found.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn get domain(addr: VSLObject) -> VSLObject
```

<details>
<summary markdown="span"> details </summary>

Get the `domain` of an email address
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn get domains(container: Array) -> Array
```

<details>
<summary markdown="span"> details </summary>

Get the `domains` of an array of email address
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn get has_debug_flag(key: PublicKey) -> bool
```

<details>
<summary markdown="span"> details </summary>

A public key may contains a `debug flag`, used for testing purpose.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn get has_dkim_result(ctx: Context) -> bool
```

<details>
<summary markdown="span"> details </summary>

Has the `ctx()` a DKIM signature verification result ?
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn get helo(context: Context) -> String
```

<details>
<summary markdown="span"> details </summary>

Get the value of the `HELO/EHLO` command sent by the client.

# Effective smtp stage

`helo` and onwards.

# Return

* `string` - the value of the `HELO/EHLO` command.

# Examples

```
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
fn get is_authenticated(context: Context) -> bool
```

<details>
<summary markdown="span"> details </summary>

Check if the client is authenticated.

# Effective smtp stage

`authenticate` stage only.

# Return

* `bool` - `true` if the client succeeded to authenticate itself, `false` otherwise.

# Example
```
#{
    authenticate: [
       action "log info" || log("info", `client authenticated: ${is_authenticated()}`),
    ]
}
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn get is_secured(context: Context) -> bool
```

<details>
<summary markdown="span"> details </summary>

Has the connection been secured under the encryption protocol SSL/TLS.

# Effective smtp stage

all of them.

# Return

* bool - `true` if the connection is secured, `false` otherwise.

# Example
```
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
fn get local_part(addr: VSLObject) -> String
```

<details>
<summary markdown="span"> details </summary>

Get the `local part` of an email address
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn get local_parts(container: Array) -> Array
```

<details>
<summary markdown="span"> details </summary>

Get the user identifier of a list of email address.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn get mail(this: Message) -> String
```

<details>
<summary markdown="span"> details </summary>

Get a copy of the whole email as a string.

# Effective smtp stage

`preq` and onwards.

# Example
```
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
fn get mail_from(context: Context) -> SharedObject
```

<details>
<summary markdown="span"> details </summary>

Get the value of the `MAIL FROM` command sent by the client.

# Effective smtp stage

`mail` and onwards.

# Return

* `address` - the sender address.

# Examples

```
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
fn get mail_timestamp(context: Context) -> OffsetDateTime
```

<details>
<summary markdown="span"> details </summary>

Get the time of reception of the email.

# Effective smtp stage

`preq` and onwards.

# Return

* `string` - the timestamp.

# Examples

```
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
fn get message_id(context: Context) -> String
```

<details>
<summary markdown="span"> details </summary>

Get the unique id of the received message.

# Effective smtp stage

`preq` and onwards.

# Return

* `string` - the message id.

# Examples

```
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
fn get rcpt(context: Context) -> SharedObject
```

<details>
<summary markdown="span"> details </summary>

Get the value of the current `RCPT TO` command sent by the client.

# Effective smtp stage

`rcpt` and onwards. Please note that `rcpt()` will always return
the last recipient received in stages after the `rcpt` stage. Therefore,
this functions is best used in the `rcpt` stage.

# Return

* `address` - the address of the received recipient.

# Examples

```
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
fn get rcpt_list(context: Context) -> Array
```

<details>
<summary markdown="span"> details </summary>

Get the list of recipients received by the client.

# Effective smtp stage

`rcpt` and onwards. Note that you will not have all recipients received
all at once in the `rcpt` stage. It is better to use this function
in the later stages.

# Return

* `Array of addresses` - the list containing all recipients.

# Examples

```
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
fn get receiver_address(smtp: Smtp) -> String
```

<details>
<summary markdown="span"> details </summary>

Get the receiver address from a smtp service.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn get receiver_policy(record: Record) -> String
```

<details>
<summary markdown="span"> details </summary>


</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn get sdid(signature: Signature) -> String
```

<details>
<summary markdown="span"> details </summary>

return the `sdid` property of the [`Signature`]
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn get server_address(context: Context) -> String
```

<details>
<summary markdown="span"> details </summary>

Get the full server address.

# Effective smtp stage

All of them.

# Return

* `string` - the server's address with the `ip:port` format.

# Example

```
#{
    connect: [
       action "log info" || log("info", `server address: ${server_address()}`),
    ]
}
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn get server_ip(context: Context) -> IpAddr
```

<details>
<summary markdown="span"> details </summary>

Get the server's ip.

# Effective smtp stage

All of them.

# Return

* `string` - the server's ip.

# Example

```
#{
    connect: [
       action "log info" || log("info", `server ip: ${server_ip()}`),
    ]
}
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn get server_name(context: Context) -> String
```

<details>
<summary markdown="span"> details </summary>

Get the name of the server.

# Effective smtp stage

All of them.

# Return

* `string` - the name of the server.

# Example
```
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
fn get server_port(context: Context) -> int
```

<details>
<summary markdown="span"> details </summary>

Get the server's port.

# Effective smtp stage

All of them.

# Return

* `string` - the server's port.

# Example
```
#{
    connect: [
       action "log info" || log("info", `server port: ${server_port()}`),
    ]
}
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn get type(credentials: Credentials) -> String
```

<details>
<summary markdown="span"> details </summary>

Get the type of the `auth` property of the connection.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn get_all_headers(message: Message) -> Array
```

<details>
<summary markdown="span"> details </summary>

Get a list of all headers.

# Return

* `array` - all of the headers found in the message.

# Effective smtp stage

All of them, although it is most useful in the `preq` stage because this
is when the email body is received.

# Examples

```
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
fn get_all_headers(message: Message, name: String) -> Array
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

# Examples

```
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
fn get_all_headers(message: Message, name: SharedObject) -> Array
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

# Examples

```
#{
    postq: [
        action "display return path" || {
            print(get_all_headers(identifier("Return-Path")));
        }
    ],
}
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn get_dmarc_record(server: Server, domain: String) -> Record
```

<details>
<summary markdown="span"> details </summary>

Get a valid DMARC record for the domain.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn get_dmarc_record(server: Server, domain: SharedObject) -> Record
```

<details>
<summary markdown="span"> details </summary>

Get a valid DMARC record for the domain.
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

# Args

* `address` - the address to extract the domain from.

# Effective smtp stage

All of them.

# Examples

```rust
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

# Args

* `rcpt_list` - the recipient list.

# Effective smtp stage

`mail` and onwards.

# Examples

```rust
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
fn get_header(message: Message, header: String) -> String
```

<details>
<summary markdown="span"> details </summary>

Get a specific header from the incoming message.

# Args

* `header` - the name of the header to get.

# Return

* `string` - the header value, or an empty string if the header was not found.

# Effective smtp stage

All of them, although it is most useful in the `preq` stage because this
is when the email body is received.

# Examples

```
#{
    postq: [
        action "display VSMTP header" || {
            print(get_header("X-VSMTP"));
        }
    ],
}
```

```
X-My-Header: 250 foo
Subject: Unit test are cool

Hello world!
; // .eml ends here

#{
  preq: [
    rule "get_header" || {
      if get_header("X-My-Header") != "250 foo"
        || get_header(identifier("Subject")) != "Unit test are cool" {
        deny();
      } else {
        accept(`${get_header("X-My-Header")} ${get_header(identifier("Subject"))}`);
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
fn get_header(message: Message, header: SharedObject) -> String
```

<details>
<summary markdown="span"> details </summary>

Get a specific header from the incoming message.

# Args

* `header` - the name of the header to get.

# Return

* `string` - the header value, or an empty string if the header was not found.

# Effective smtp stage

All of them, although it is most useful in the `preq` stage because this
is when the email body is received.

# Examples

```
#{
    postq: [
        action "display VSMTP header" || {
            print(get_header(identifier("X-VSMTP")));
        }
    ],
}
```

```
X-My-Header: 250 foo
Subject: Unit test are cool

Hello world!
; // .eml ends here

#{
  preq: [
    rule "get_header" || {
      if get_header("X-My-Header") != "250 foo"
        || get_header(identifier("Subject")) != "Unit test are cool" {
        deny();
      } else {
        accept(`${get_header("X-My-Header")} ${get_header(identifier("Subject"))}`);
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
fn get_header_untouched(this: Message, name: String) -> Array
```

<details>
<summary markdown="span"> details </summary>


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

# Args

* `address` - the address to extract the local part from.

# Effective smtp stage

All of them.

# Examples

```rust
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

# Args

* `rcpt_list` - the recipient list.

# Effective smtp stage

`mail` and onwards.

# Examples

```rust
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
fn get_private_keys(server: Server, sdid: String) -> Array
```

<details>
<summary markdown="span"> details </summary>

Get the list of DKIM private keys associated with this sdid
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn get_public_key(server: Server, signature: Signature, on_multiple_key_records: String) -> ?
```

<details>
<summary markdown="span"> details </summary>

Get the list of public keys associated with this [`Signature`]

The current implementation will make a TXT query on the dns of the signer

`on_multiple_key_records` value can be `first` or `cycle` :
* `first` return the first key found (one element array)
* `cycle` return all the keys found
</details>

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
fn get_root_domain(domain: SharedObject) -> String
```

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn handle_dkim_error(err: ?) -> String
```

<details>
<summary markdown="span"> details </summary>

get the dkim status from an error produced by this module

# Error
* The given parameter is not a Map.
* `type` field not found in parameter / is not a string.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn has_expired(signature: Signature, epsilon: int) -> bool
```

<details>
<summary markdown="span"> details </summary>

Has the signature expired?

return `true` if the argument are invalid (`epsilon` is negative)
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn has_header(message: Message, header: SharedObject) -> bool
```

<details>
<summary markdown="span"> details </summary>

Checks if the message contains a specific header.

# Args

* `header` - the name of the header to search.

# Effective smtp stage

All of them, although it is most useful in the `preq` stage because the
email is received at this point.

# Examples

```
#{
    postq: [
        action "check for VSMTP header" || {
            if has_header(identifier("X-VSMTP")) {
                log("info", "incoming message could be from another vsmtp server");
            }
        }
    ],
}
```

```
// Message example.
"X-My-Header: foo\r\n",
"Subject: Unit test are cool\r\n",
"\r\n",
"Hello world!\r\n",

#{
  preq: [
    rule "check if header exists" || {
      if has_header("X-My-Header") && has_header(identifier("Subject")) {
        accept();
      } else {
        deny();
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
fn has_header(message: Message, header: String) -> bool
```

<details>
<summary markdown="span"> details </summary>

Checks if the message contains a specific header.

# Args

* `header` - the name of the header to search.

# Effective smtp stage

All of them, although it is most useful in the `preq` stage because the
email is received at this point.

# Examples

```
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

```
// Message example.
"X-My-Header: foo\r\n",
"Subject: Unit test are cool\r\n",
"\r\n",
"Hello world!\r\n",

#{
  preq: [
    rule "check if header exists" || {
      if has_header("X-My-Header") && has_header(identifier("Subject")) {
        accept();
      } else {
        deny();
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

```js
#{
    preq: [
       action "append info header" || {
            append_header("X-VSMTP", `email received by ${hostname()}.`);
       }
    ]
}
```

```
# vsmtp_test::vsl::run(
# |builder| Ok(builder.add_root_incoming_rules(r#"
#{
  connect: [
    rule "hostname" || {
      accept(`250 ${hostname()}`);
    }
  ]
}
# "#)?.build()));
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn identifier(identifier: String) -> VSLObject
```

<details>
<summary markdown="span"> details </summary>

a user identifier.
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
fn ip4(ip: String) -> VSLObject
```

<details>
<summary markdown="span"> details </summary>

Build an ip4 address. (a.b.c.d)
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn ip6(ip: String) -> VSLObject
```

<details>
<summary markdown="span"> details </summary>

Build an ip6 address. (x:x:x:x:x:x:x:x)
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn log(level: SharedObject, message: SharedObject)
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
    preq: [
       action "log info" || log("info", "this is an informational log."),
    ]
}
```

```
#{
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
fn log(level: SharedObject, message: String)
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
    preq: [
       action "log info" || log("info", "this is an informational log."),
    ]
}
```

```
#{
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
    preq: [
       action "log info" || log("info", "this is an informational log."),
    ]
}
```

```
#{
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
    preq: [
       action "log info" || log("info", "this is an informational log."),
    ]
}
```

```
#{
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
fn lookup(server: Server, name: String) -> Array
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

```rust
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
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
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

```js
#{
    rcpt: [
       action "perform lookup" || {
            let ips = lookup(fqdn("example.com"));

            print(`ips found for ${domain}`);
            for ip in ips {
                print(`- ${ip}`);
            }
       }
    ]
}
```

```
# vsmtp_test::vsl::run(
# |builder| Ok(builder.add_root_incoming_rules(r#"
#{
  preq: [
    action "lookup recipients" || {
      let domain = fqdn("gmail.com");
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


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn maildir(context: Context, rcpt: String) -> ()
```

<details>
<summary markdown="span"> details </summary>

Set the delivery method to maildir for a recipient.
After all rules are evaluated, the email will be stored
locally in the `~/Maildir/new/` folder of the recipient's user if it exists on the server.

# Args

* `rcpt` - the recipient to apply the method to.

# Effective smtp stage

All of them.

# Examples
```
#{
    delivery: [
       action "setup maildir" || maildir("john.doe@example.com"),
    ]
}
```

```
 #{
   rcpt: [
     action "setup maildir" || {
         const doe = address("doe@example.com");
         add_rcpt_envelop(doe);
         add_rcpt_envelop("a@example.com");
         maildir(doe);
         maildir("a@example.com");
     },
   ],
 }

```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn maildir(context: Context, rcpt: SharedObject) -> ()
```

<details>
<summary markdown="span"> details </summary>

Set the delivery method to maildir for a recipient.
After all rules are evaluated, the email will be stored
locally in the `~/Maildir/new/` folder of the recipient's user if it exists on the server.

# Args

* `rcpt` - the recipient to apply the method to.

# Effective smtp stage

All of them.

# Example
```
#{
    delivery: [
       action "setup maildir" || maildir(address("john.doe@example.com")),
    ]
}
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn maildir_all(context: Context) -> ()
```

<details>
<summary markdown="span"> details </summary>

Set the delivery method to maildir for all recipients.
After all rules are evaluated, the email will be stored
locally in each `~/Maildir/new` folder of they respective recipient
if they exists on the server.

# Effective smtp stage

All of them.

# Examples

```
#{
    delivery: [
       action "setup mbox" || mbox_all(),
    ]
}
```

```
#{
  rcpt: [
    action "setup maildir" || {
        const doe = address("doe@example.com");
        add_rcpt_envelop(doe);
        add_rcpt_envelop("a@example.com");
        maildir_all();
    },
  ],
}

```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn mbox(context: Context, rcpt: String) -> ()
```

<details>
<summary markdown="span"> details </summary>

Set the delivery method to mbox for a recipient.
After all rules are evaluated, the email will be stored
locally in the mail box of the recipient if it exists on the server.

# Args

* `rcpt` - the recipient to apply the method to.

# Effective smtp stage

All of them.

# Examples

```
#{
    delivery: [
       action "setup mbox" || mbox("john.doe@example.com"),
    ]
}
```

```
 #{
   rcpt: [
     action "setup mbox" || {
         const doe = address("doe@example.com");
         add_rcpt_envelop(doe);
         add_rcpt_envelop("a@example.com");
         mbox(doe);
         mbox("a@example.com");
     },
   ],
 }

```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn mbox(context: Context, rcpt: SharedObject) -> ()
```

<details>
<summary markdown="span"> details </summary>

Set the delivery method to mbox for a recipient.
After all rules are evaluated, the email will be stored
locally in the mail box of the recipient if it exists on the server.

# Args

* `rcpt` - the recipient to apply the method to.

# Effective smtp stage

All of them.

# Example
```
#{
    delivery: [
       action "setup mbox" || mbox(address("john.doe@example.com")),
    ]
}
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn mbox_all(context: Context) -> ()
```

<details>
<summary markdown="span"> details </summary>

Set the delivery method to mbox for all recipients.
After all rules are evaluated, the email will be stored
locally in the mail box of all recipients if they exists on the server.

# Effective smtp stage

All of them.

# Examples

```
#{
    delivery: [
       action "setup mbox" || mbox_all(),
    ]
}
```

```
 #{
   rcpt: [
     action "setup mbox" || {
         const doe = address("doe@example.com");
         add_rcpt_envelop(doe);
         add_rcpt_envelop("a@example.com");
         mbox_all();
     },
   ],
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

# Note
This is used internally to provide encapsulation of vsl's features.
You should not use this function directly.

# Return

* `the message`

# Effective smtp stage

all of them.

# Examples

```rust
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
fn parse_rfc5322_from(message: Message) -> SharedObject
```

<details>
<summary markdown="span"> details </summary>

Get the address of the sender in the message body, also known as RFC5322.From
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn parse_signature(input: String) -> Signature
```

<details>
<summary markdown="span"> details </summary>

create a [`Signature`] from a `DKIM-Signature` header
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn prepend_header(message: Message, header: String, value: String) -> ()
```

<details>
<summary markdown="span"> details </summary>

Add a new header on top all other headers in the message.

# Args

* `header` - the name of the header to prepend.
* `value` - the value of the header to prepend.

# Effective smtp stage

All of them. Even though the email is not received at the current stage,
vsmtp stores new headers and will add them on top of the ones received once
the `preq` stage is reached.

# Examples

```
#{
    postq: [
        action "prepend a header" || {
            prepend_header("X-JOHN", "received by john's server.");
        }
    ],
}
```

```
"X-My-Header: 250 foo\r\n",
"Subject: Unit test are cool\r\n",
"\r\n",
"Hello world!\r\n",

#{
  preq: [
    rule "prepend_header" || {
      prepend_header("X-My-Header-2", "bar");
      prepend_header("X-My-Header-3", identifier("baz"));
    }
  ]
}
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn prepend_header(message: Message, header: String, value: SharedObject) -> ()
```

<details>
<summary markdown="span"> details </summary>

Add a new header on top all other headers in the message.

# Args

* `header` - the name of the header to prepend.
* `value` - the value of the header to prepend.

# Effective smtp stage

All of them. Even though the email is not received at the current stage,
vsmtp stores new headers and will add them on top of the ones received once
the `preq` stage is reached.

# Examples

```
#{
    postq: [
        action "prepend a header" || {
            prepend_header("X-JOHN", "received by john's server.");
        }
    ],
}
```

```
"X-My-Header: 250 foo\r\n",
"Subject: Unit test are cool\r\n",
"\r\n",
"Hello world!\r\n",

#{
  preq: [
    rule "prepend_header" || {
      prepend_header("X-My-Header-2", "bar");
      prepend_header("X-My-Header-3", identifier("baz"));
    }
  ]
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


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn regex(regex: String) -> VSLObject
```

<details>
<summary markdown="span"> details </summary>

a regex (^[a-z0-9.]+@foo.com$)
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn remove_header(message: Message, header: SharedObject) -> bool
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

# Examples

```
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

```
"Subject: The initial header value\r\n",
"\r\n",
"Hello world!\r\n",

#{
  preq: [
    rule "remove_header" || {
      remove_header("Subject");
      if has_header("Subject") { return deny(); }

      prepend_header("Subject-2", "Rust is good");
      remove_header(identifier("Subject-2"));

      prepend_header("Subject-3", "Rust is good !!!!!");

      accept(`250 ${get_header("Subject-3")}`);
    }
  ]
}
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn remove_header(message: Message, header: String) -> bool
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

# Examples

```
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

```
"Subject: The initial header value\r\n",
"\r\n",
"Hello world!\r\n",

#{
  preq: [
    rule "remove_header" || {
      remove_header("Subject");
      if has_header("Subject") { return deny(); }

      prepend_header("Subject-2", "Rust is good");
      remove_header(identifier("Subject-2"));

      prepend_header("Subject-3", "Rust is good !!!!!");

      accept(`250 ${get_header("Subject-3")}`);
    }
  ]
}
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn remove_rcpt_envelop(context: Context, addr: String) -> ()
```

<details>
<summary markdown="span"> details </summary>

Remove a recipient from the envelop. Note that this does not remove
the recipient from the `To` header. Use `remove_rcpt_message` for that.

# Args

* `rcpt` - the recipient to remove.

# Effective smtp stage

All of them.

# Examples

```
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
fn remove_rcpt_envelop(context: Context, addr: SharedObject) -> ()
```

<details>
<summary markdown="span"> details </summary>

Remove a recipient from the envelop. Note that this does not remove
the recipient from the `To` header. Use `remove_rcpt_message` for that.

# Args

* `rcpt` - the recipient to remove.

# Effective smtp stage

All of them.

# Examples

```
#{
    preq: [
       // never deliver to "john.doe@example.com".
       action "rewrite envelop" || remove_rcpt_envelop(address("john.doe@example.com")),
    ]
}
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn remove_rcpt_message(message: Message, addr: String) -> ()
```

<details>
<summary markdown="span"> details </summary>

Remove a recipient from the `To` header of the message.

# Args

* `addr` - the recipient to remove to the `To` header.

# Effective smtp stage

`preq` and onwards.

# Examples

```
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
fn remove_rcpt_message(message: Message, addr: SharedObject) -> ()
```

<details>
<summary markdown="span"> details </summary>

Remove a recipient from the `To` header of the message.

# Args

* `addr` - the recipient to remove to the `To` header.

# Effective smtp stage

`preq` and onwards.

# Examples

```
#{
    preq: [
       action "update recipients" || remove_rcpt_message(address("john.doe@example.com")),
    ]
}
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn rename_header(message: Message, old: String, new: String) -> ()
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

# Examples

```
#{
    postq: [
        action "rename header" || {
            rename_header("X-To-Rename", "X-Renamed");
        }
    ],
}
```

```
"Subject: The initial header value\r\n",
"\r\n",
"Hello world!\r\n",

#{
  preq: [
    rule "rename_header" || {
      rename_header("Subject", "bob");
      if has_header("Subject") { return deny(); }

      rename_header("bob", identifier("Subject"));
      if has_header("bob") { return deny(); }

      rename_header(identifier("Subject"), "foo");
      if has_header("Subject") { return deny(); }

      rename_header(identifier("foo"), identifier("Subject"));
      if has_header("foo") { return deny(); }

      accept(`250 ${get_header("Subject")}`);
    }
  ]
}
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn rename_header(message: Message, old: String, new: SharedObject) -> ()
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

# Examples

```
#{
    postq: [
        action "rename header" || {
            rename_header("X-To-Rename", "X-Renamed");
        }
    ],
}
```

```
"Subject: The initial header value\r\n",
"\r\n",
"Hello world!\r\n",

#{
  preq: [
    rule "rename_header" || {
      rename_header("Subject", "bob");
      if has_header("Subject") { return deny(); }

      rename_header("bob", identifier("Subject"));
      if has_header("bob") { return deny(); }

      rename_header(identifier("Subject"), "foo");
      if has_header("Subject") { return deny(); }

      rename_header(identifier("foo"), identifier("Subject"));
      if has_header("foo") { return deny(); }

      accept(`250 ${get_header("Subject")}`);
    }
  ]
}
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn rename_header(message: Message, old: SharedObject, new: SharedObject) -> ()
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

# Examples

```
#{
    postq: [
        action "rename header" || {
            rename_header("X-To-Rename", "X-Renamed");
        }
    ],
}
```

```
"Subject: The initial header value\r\n",
"\r\n",
"Hello world!\r\n",

#{
  preq: [
    rule "rename_header" || {
      rename_header("Subject", "bob");
      if has_header("Subject") { return deny(); }

      rename_header("bob", identifier("Subject"));
      if has_header("bob") { return deny(); }

      rename_header(identifier("Subject"), "foo");
      if has_header("Subject") { return deny(); }

      rename_header(identifier("foo"), identifier("Subject"));
      if has_header("foo") { return deny(); }

      accept(`250 ${get_header("Subject")}`);
    }
  ]
}
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn rename_header(message: Message, old: SharedObject, new: String) -> ()
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

# Examples

```
#{
    postq: [
        action "rename header" || {
            rename_header("X-To-Rename", "X-Renamed");
        }
    ],
}
```

```
"Subject: The initial header value\r\n",
"\r\n",
"Hello world!\r\n",

#{
  preq: [
    rule "rename_header" || {
      rename_header("Subject", "bob");
      if has_header("Subject") { return deny(); }

      rename_header("bob", identifier("Subject"));
      if has_header("bob") { return deny(); }

      rename_header(identifier("Subject"), "foo");
      if has_header("Subject") { return deny(); }

      rename_header(identifier("foo"), identifier("Subject"));
      if has_header("foo") { return deny(); }

      accept(`250 ${get_header("Subject")}`);
    }
  ]
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

# Args

* `new_addr` - the new sender address to set.

# Effective smtp stage

`preq` and onwards.

# Examples

```rust
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
fn rewrite_mail_from_envelop(context: Context, new_addr: SharedObject) -> ()
```

<details>
<summary markdown="span"> details </summary>

Rewrite the sender received from the `MAIL FROM` command.

# Args

* `new_addr` - the new sender address to set.

# Effective smtp stage

`mail` and onwards.

# Examples

```
#{
    preq: [
       action "rewrite envelop" || rewrite_mail_from_envelop(address("unknown@example.com")),
    ]
}
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn rewrite_mail_from_envelop(context: Context, new_addr: String) -> ()
```

<details>
<summary markdown="span"> details </summary>

Rewrite the sender received from the `MAIL FROM` command.

# Args

* `new_addr` - the new string sender address to set.

# Effective smtp stage

`mail` and onwards.

# Examples

```
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
fn rewrite_mail_from_message(message: Message, new_addr: String) -> ()
```

<details>
<summary markdown="span"> details </summary>

Change the sender's address in the `From` header of the message.

# Args

* `new_addr` - the new sender address to set.

# Effective smtp stage

`preq` and onwards.

# Examples

```
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
fn rewrite_mail_from_message(message: Message, new_addr: SharedObject) -> ()
```

<details>
<summary markdown="span"> details </summary>

Change the sender's address in the `From` header of the message.

# Args

* `new_addr` - the new sender address to set.

# Effective smtp stage

`preq` and onwards.

# Examples

```
#{
    preq: [
       action "replace sender" || rewrite_mail_from_message(address("john.server@example.com")),
    ]
}
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn rewrite_rcpt_envelop(context: Context, old_addr: String, new_addr: SharedObject) -> ()
```

<details>
<summary markdown="span"> details </summary>

Replace a recipient received by a `RCPT TO` command.

# Args

* `old_addr` - the recipient to replace.
* `new_addr` - the new address to use when replacing `old_addr`.

# Effective smtp stage

`rcpt` and onwards.

# Examples

```
#{
    preq: [
       action "rewrite envelop" || rewrite_rcpt_envelop("john.doe@example.com", address("john.main@example.com")),
    ]
}
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn rewrite_rcpt_envelop(context: Context, old_addr: SharedObject, new_addr: SharedObject) -> ()
```

<details>
<summary markdown="span"> details </summary>

Replace a recipient received by a `RCPT TO` command.

# Args

* `old_addr` - the recipient to replace.
* `new_addr` - the new address to use when replacing `old_addr`.

# Effective smtp stage

`rcpt` and onwards.

# Examples

```
#{
    preq: [
       action "rewrite envelop" || rewrite_rcpt_envelop(address("john.doe@example.com"), address("john.main@example.com")),
    ]
}
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn rewrite_rcpt_envelop(context: Context, old_addr: String, new_addr: String) -> ()
```

<details>
<summary markdown="span"> details </summary>

Replace a recipient received by a `RCPT TO` command.

# Args

* `old_addr` - the recipient to replace.
* `new_addr` - the new address to use when replacing `old_addr`.

# Effective smtp stage

`rcpt` and onwards.

# Examples

```
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
fn rewrite_rcpt_envelop(context: Context, old_addr: SharedObject, new_addr: String) -> ()
```

<details>
<summary markdown="span"> details </summary>

Replace a recipient received by a `RCPT TO` command.

# Args

* `old_addr` - the recipient to replace.
* `new_addr` - the new address to use when replacing `old_addr`.

# Effective smtp stage

`rcpt` and onwards.

# Examples

```
#{
    preq: [
       action "rewrite envelop" || rewrite_rcpt_envelop(address("john.doe@example.com"), "john.main@example.com"),
    ]
}
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn rewrite_rcpt_message(message: Message, old_addr: String, new_addr: SharedObject) -> ()
```

<details>
<summary markdown="span"> details </summary>

Replace a recipient by an other in the `To` header of the message.

# Args

* `old_addr` - the recipient to replace.
* `new_addr` - the new address to use when replacing `old_addr`.

# Effective smtp stage

`preq` and onwards.

# Examples

```
#{
    preq: [
       action "rewrite recipient" || rewrite_rcpt_message("john.doe@example.com", address("john-mta@example.com")),
    ]
}
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn rewrite_rcpt_message(message: Message, old_addr: SharedObject, new_addr: SharedObject) -> ()
```

<details>
<summary markdown="span"> details </summary>

Replace a recipient by an other in the `To` header of the message.

# Args

* `old_addr` - the recipient to replace.
* `new_addr` - the new address to use when replacing `old_addr`.

# Effective smtp stage

`preq` and onwards.

# Examples

```
#{
    preq: [
       action "rewrite recipient" || rewrite_rcpt_message(address("john.doe@example.com"), address("john-mta@example.com")),
    ]
}
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn rewrite_rcpt_message(message: Message, old_addr: SharedObject, new_addr: String) -> ()
```

<details>
<summary markdown="span"> details </summary>

Replace a recipient by an other in the `To` header of the message.

# Args

* `old_addr` - the recipient to replace.
* `new_addr` - the new address to use when replacing `old_addr`.

# Effective smtp stage

`preq` and onwards.

# Examples

```
#{
    preq: [
       action "rewrite recipient" || rewrite_rcpt_message(address("john.doe@example.com"), "john-mta@example.com"),
    ]
}
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn rewrite_rcpt_message(message: Message, old_addr: String, new_addr: String) -> ()
```

<details>
<summary markdown="span"> details </summary>

Replace a recipient by an other in the `To` header of the message.

# Args

* `old_addr` - the recipient to replace.
* `new_addr` - the new address to use when replacing `old_addr`.

# Effective smtp stage

`preq` and onwards.

# Examples

```
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
fn rg4(range: String) -> VSLObject
```

<details>
<summary markdown="span"> details </summary>

an ip v4 range. (a.b.c.d/range)
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn rg6(range: String) -> VSLObject
```

<details>
<summary markdown="span"> details </summary>

an ip v6 range. (x:x:x:x:x:x:x:x/range)
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn rlookup(server: Server, name: String) -> Array
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


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
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


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn run(cmd: Cmd) -> Map
```

<details>
<summary markdown="span"> details </summary>

Execute the given command.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn run(cmd: Cmd, args: Array) -> Map
```

<details>
<summary markdown="span"> details </summary>

Execute the given command with dynamic arguments.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn set_header(message: Message, header: String, value: String) -> ()
```

<details>
<summary markdown="span"> details </summary>

Replace an existing header value by a new value, or append a new header
to the message.

# Args

* `header` - the name of the header to set or add.
* `value` - the value of the header to set or add.

# Effective smtp stage

All of them. Even though the email is not received at the current stage,
vsmtp stores new headers and will add them on top to the ones received once
the `preq` stage is reached.

Be aware that if you want to set a header value from the original message,
you must use `set_header` in the `preq` stage and onwards.

# Examples

```
#{
    postq: [
        action "update subject" || {
            let subject = get_header("Subject");
            set_header("Subject", `${subject} (analyzed by vsmtp)`);
        }
    ],
}
```

```
"Subject: The initial header value\r\n",
"\r\n",
"Hello world!\r\n",

#{
  preq: [
    rule "set_header" || {
      set_header("Subject", "The header value has been updated");
      set_header("Subject", identifier("The header value has been updated again"));
      accept(`250 ${get_header("Subject")}`);
    }
  ]
}
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn set_header(message: Message, header: String, value: SharedObject) -> ()
```

<details>
<summary markdown="span"> details </summary>

Replace an existing header value by a new value, or append a new header
to the message.

# Args

* `header` - the name of the header to set or add.
* `value` - the value of the header to set or add.

# Effective smtp stage

All of them. Even though the email is not received at the current stage,
vsmtp stores new headers and will add them on top to the ones received once
the `preq` stage is reached.

Be aware that if you want to set a header value from the original message,
you must use `set_header` in the `preq` stage and onwards.

# Examples

```
#{
    postq: [
        action "update subject" || {
            let subject = get_header("Subject");
            set_header("Subject", `${subject} (analyzed by vsmtp)`);
        }
    ],
}
```

```
"Subject: The initial header value\r\n",
"\r\n",
"Hello world!\r\n",

#{
  preq: [
    rule "set_header" || {
      set_header("Subject", "The header value has been updated");
      set_header("Subject", identifier("The header value has been updated again"));
      accept(`250 ${get_header("Subject")}`);
    }
  ]
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

# Module:Security
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

# Args

* `selector` - the DNS selector to expose the public key & for the verifier
* `private_key` - the private key to sign the mail,
    associated with the public key in the `selector._domainkey.sdid` DNS record
* `headers_field` - list of headers to sign
* `canonicalization` - the canonicalization algorithm to use (ex: "simple/relaxed")

# Effective smtp stage

`preq` and onwards.

# Example

```
#{
  preq: [
    action "sign dkim" || {
      sign_dkim("2022-09", ["From", "To", "Date", "Subject", "From"], "simple/relaxed");
    },
  ]
}
```

# Module:Security
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn smtp(parameters: Map) -> Smtp
```

<details>
<summary markdown="span"> details </summary>

Build a new SMTP service.
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

# Note
This is used internally to provide encapsulation of vsl's features.
You should not use this function directly.

# Return

* `the server api`

# Effective smtp stage

all of them.

# Examples

```rust
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
fn store_dkim(ctx: Context, result: Map) -> ()
```

<details>
<summary markdown="span"> details </summary>

Store the result produced by the DKIM signature verification in the `ctx()`.

# Error
* The `status` field is missing in the DKIM verification results.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn time() -> String
```

<details>
<summary markdown="span"> details </summary>

Get the current time.

### Return

* `string` - the current time.

### Effective smtp stage

All of them.

### Examples

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
fn to_debug(cmd: Smtp) -> String
```

<details>
<summary markdown="span"> details </summary>


</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn to_debug(cmd: Cmd) -> String
```

<details>
<summary markdown="span"> details </summary>


</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn to_debug(this: VSLObject) -> String
```

<details>
<summary markdown="span"> details </summary>

Convert a `SharedObject` to a debug string
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn to_debug(context: Context) -> String
```

<details>
<summary markdown="span"> details </summary>

Convert a `Context` to a debug string.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn to_debug(context: Server) -> String
```

<details>
<summary markdown="span"> details </summary>

Convert a `Server` to a debug string.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn to_debug(this: OffsetDateTime) -> String
```

<details>
<summary markdown="span"> details </summary>

Convert a `time::OffsetDateTime` to a `String`
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn to_debug(status: Status) -> String
```

<details>
<summary markdown="span"> details </summary>

Convert a `Status` to a debug string
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn to_debug(record: Record) -> String
```

<details>
<summary markdown="span"> details </summary>

Produce a debug output for the parsed [`dmarc::Record`]
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn to_string(cmd: Smtp) -> String
```

<details>
<summary markdown="span"> details </summary>


</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn to_string(cmd: Cmd) -> String
```

<details>
<summary markdown="span"> details </summary>


</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn to_string(this: VSLObject) -> String
```

<details>
<summary markdown="span"> details </summary>

Convert a `SharedObject` to a `String`
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn to_string(_: Context) -> String
```

<details>
<summary markdown="span"> details </summary>

Convert a `Context` to a `String`.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn to_string(_: Server) -> String
```

<details>
<summary markdown="span"> details </summary>

Convert a `Server` to a `String`.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn to_string(status: Status) -> String
```

<details>
<summary markdown="span"> details </summary>

Convert a `Status` to a `String`
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn to_string(this: OffsetDateTime) -> String
```

<details>
<summary markdown="span"> details </summary>

Convert a `time::OffsetDateTime` to a `String`
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn user_exist(name: String) -> bool
```

<details>
<summary markdown="span"> details </summary>

send a mail from a template.
Check if a user exists on this server.

### Args

* `name` - the name of the user.

### Return

* `bool` - true if the user exists, false otherwise.

### Effective smtp stage

All of them.

### Examples

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


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
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


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn verify_dkim()
```

<details>
<summary markdown="span"> details </summary>

Verify the `DKIM-Signature` header(s) in the mail and produce a `Authentication-Results`.
If this function has already been called once, it will return the result of the previous call.
see https://datatracker.ietf.org/doc/html/rfc6376

# Return

* a DkimResult object

# Effective smtp stage

`preq` and onwards.

# Example

```
#{
  preq: [
    action "check dkim" || { verify_dkim(); },
  ]
}
````

</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn verify_dkim(message: Message, signature: Signature, key: PublicKey) -> ()
```

<details>
<summary markdown="span"> details </summary>

Operate the hashing of the `message`'s headers and body, and compare the result with the
`signature` and `key` data.

# Examples

```js
// The message received.
let msg = r#"
Received: from github.com (hubbernetes-node-54a15d2.ash1-iad.github.net [10.56.202.84])
	by smtp.github.com (Postfix) with ESMTPA id 19FB45E0B6B
	for <mlala@negabit.com>; Wed, 26 Oct 2022 14:30:51 -0700 (PDT)
DKIM-Signature: v=1; a=rsa-sha256; c=relaxed/relaxed; d=github.com;
	s=pf2014; t=1666819851;
	bh=7gTTczemS/Aahap1SpEnunm4pAPNuUIg7fUzwEx0QUA=;
	h=Date:From:To:Subject:From;
	b=eAufMk7uj4R+bO5Nr4DymffdGdbrJNza1+eykatgZED6tBBcMidkMiLSnP8FyVCS9
	 /GSlXME6/YffAXg4JEBr2lN3PuLIf94S86U3VckuoQQQe1LPtHlnGW5ZwJgi6DjrzT
	 klht/6Pn1w3a2jdNSDccWhk5qlSOQX9JKnE7UD58=
Date: Wed, 26 Oct 2022 14:30:51 -0700
From: Mathieu Lala <noreply@github.com>
To: mlala@negabit.com
Message-ID: <viridIT/vSMTP/push/refs/heads/test/rule-engine/000000-c6459a@github.com>
Subject: [viridIT/vSMTP] c6459a: test: add test on message
Mime-Version: 1.0
Content-Type: text/plain;
 charset=UTF-8
Content-Transfer-Encoding: 7bit
Approved: =?UTF-8?Q?hello_there_=F0=9F=91=8B?=
X-GitHub-Recipient-Address: mlala@negabit.com
X-Auto-Response-Suppress: All

  Branch: refs/heads/test/rule-engine
  Home:   https://github.com/viridIT/vSMTP
  Commit: c6459a4946395ba90182ce7181bdbc327994c038
      https://github.com/viridIT/vSMTP/commit/c6459a4946395ba90182ce7181bdbc327994c038
  Author: Mathieu Lala <m.lala@viridit.com>
  Date:   2022-10-26 (Wed, 26 Oct 2022)

  Changed paths:
    M src/vsmtp/vsmtp-rule-engine/src/api/message.rs
    M src/vsmtp/vsmtp-rule-engine/src/lib.rs
    M src/vsmtp/vsmtp-test/src/vsl.rs

  Log Message:
  -----------
  test: add test on message


"#;
# let msg = vsmtp_mail_parser::MessageBody::try_from(msg[1..].replace("\n", "\r\n").as_str()).unwrap();

# let states = vsmtp_test::vsl::run_with_msg(
#    |builder| Ok(builder.add_root_incoming_rules(r#"
 // Rules
 #{
   preq: [
     rule "verify_dkim" || {
       verify_dkim();
       if !get_header("Authentication-Results").contains("dkim=pass") {
         return deny();
       }
       // the result of dkim verification is cached, so this call will
       // not recompute the signature and recreate a header
       verify_dkim();

       // FIXME: should be one
       if count_header("Authentication-Results") != 2 {
         return deny();
       }

       accept();
     }
   ]
 }
# "#)?.build()), Some(msg));
# use vsmtp_common::{status::Status, CodeID};
# use vsmtp_rule_engine::ExecutionStage;
# assert_eq!(states[&ExecutionStage::PreQ].2, Status::Accept(either::Left(CodeID::Ok)));
```

Changing the header `Subject` will result in a dkim verification failure.

```js
// The message received.
let msg = r#"
Received: from github.com (hubbernetes-node-54a15d2.ash1-iad.github.net [10.56.202.84])
	by smtp.github.com (Postfix) with ESMTPA id 19FB45E0B6B
	for <mlala@negabit.com>; Wed, 26 Oct 2022 14:30:51 -0700 (PDT)
DKIM-Signature: v=1; a=rsa-sha256; c=relaxed/relaxed; d=github.com;
	s=pf2014; t=1666819851;
	bh=7gTTczemS/Aahap1SpEnunm4pAPNuUIg7fUzwEx0QUA=;
	h=Date:From:To:Subject:From;
	b=eAufMk7uj4R+bO5Nr4DymffdGdbrJNza1+eykatgZED6tBBcMidkMiLSnP8FyVCS9
	 /GSlXME6/YffAXg4JEBr2lN3PuLIf94S86U3VckuoQQQe1LPtHlnGW5ZwJgi6DjrzT
	 klht/6Pn1w3a2jdNSDccWhk5qlSOQX9JKnE7UD58=
Date: Wed, 26 Oct 2022 14:30:51 -0700
From: Mathieu Lala <noreply@github.com>
To: mlala@negabit.com
Message-ID: <viridIT/vSMTP/push/refs/heads/test/rule-engine/000000-c6459a@github.com>
Subject: Changing the header produce an invalid dkim verification
Mime-Version: 1.0
Content-Type: text/plain;
 charset=UTF-8
Content-Transfer-Encoding: 7bit
Approved: =?UTF-8?Q?hello_there_=F0=9F=91=8B?=
X-GitHub-Recipient-Address: mlala@negabit.com
X-Auto-Response-Suppress: All

  Branch: refs/heads/test/rule-engine
  Home:   https://github.com/viridIT/vSMTP
  Commit: c6459a4946395ba90182ce7181bdbc327994c038
      https://github.com/viridIT/vSMTP/commit/c6459a4946395ba90182ce7181bdbc327994c038
  Author: Mathieu Lala <m.lala@viridit.com>
  Date:   2022-10-26 (Wed, 26 Oct 2022)

  Changed paths:
    M src/vsmtp/vsmtp-rule-engine/src/api/message.rs
    M src/vsmtp/vsmtp-rule-engine/src/lib.rs
    M src/vsmtp/vsmtp-test/src/vsl.rs

  Log Message:
  -----------
  test: add test on message
"#;

let rules = r"#{
    preq: [
      rule "verify_dkim" || {
        verify_dkim();
        if !get_header("Authentication-Results").contains("dkim=fail") {
          return deny();
        }
        accept();
      }
    ]
}"#;

```
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
fn write(srv: Server, mut ctx: Context, message: Message, dir: String) -> ()
```

<details>
<summary markdown="span"> details </summary>

Export the current raw message to a file as an `eml` file.
The message id of the email is used to name the file.

# Args

* `dir` - the directory where to store the email. Relative to the
application path.

# Effective smtp stage

`preq` and onwards.

# Examples

```
#{
    preq: [
       action "write to file" || write("archives"),
    ]
}
```
</details>

</div>
</br>

