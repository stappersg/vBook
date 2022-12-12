# global



<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> != </h2>

```rust,ignore
fn !=(this: SharedObject, other: SharedObject) -> bool
fn !=(this: SharedObject, s: String) -> bool
fn !=(this: String, other: SharedObject) -> bool
fn !=(in1: Status, in2: Status) -> bool
```

<details>
<summary markdown="span"> details </summary>

Operator `!=` for `SharedObject`
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> == </h2>

```rust,ignore
fn ==(this: SharedObject, other: SharedObject) -> bool
fn ==(this: String, other: SharedObject) -> bool
fn ==(in1: Status, in2: Status) -> bool
```

<details>
<summary markdown="span"> details </summary>

Operator `==` for `SharedObject`
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> accept </h2>

```rust,ignore
fn accept(code: String) -> Status
fn accept(code: SharedObject) -> Status
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


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> add_rcpt_envelop </h2>

```rust,ignore
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


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> add_rcpt_message </h2>

```rust,ignore
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


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> append_header </h2>

```rust,ignore
fn append_header(message: Message, header: String, value: String) -> ()
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


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> bcc </h2>

```rust,ignore
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

```
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


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> check_spf </h2>

```rust,ignore
fn check_spf(header: ?)
fn check_spf(header: ?, policy: ?)
fn check_spf(ctx: Context, srv: Server) -> Map
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


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> cmd </h2>

```rust,ignore
fn cmd(parameters: Map) -> Cmd

```

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> code </h2>

```rust,ignore
fn code(code: int, enhanced: String, text: String) -> VSLObject

```

<details>
<summary markdown="span"> details </summary>

A SMTP code with the code and message as parameter and an enhanced code.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> contains </h2>

```rust,ignore
fn contains(this: SharedObject, s: String) -> bool
fn contains(map: Map, object: SharedObject) -> bool
```

<details>
<summary markdown="span"> details </summary>

Operator `contains`
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> count_header </h2>

```rust,ignore
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

```
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

<h2 class="func-name"> <code>fn</code> deliver </h2>

```rust,ignore
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


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> deny </h2>

```rust,ignore
fn deny() -> Status
fn deny(code: String) -> Status
fn deny(code: SharedObject) -> Status
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


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> dump </h2>

```rust,ignore
fn dump(srv: Server, mut ctx: Context, dir: String) -> ()

```

<details>
<summary markdown="span"> details </summary>

write the content of the current email with it's metadata in a json file.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> faccept </h2>

```rust,ignore
fn faccept(code: String) -> Status
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


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> forward </h2>

```rust,ignore
fn forward(context: Context, rcpt: String, forward: SharedObject) -> ()
fn forward(context: Context, rcpt: SharedObject, forward: SharedObject) -> ()
fn forward(context: Context, rcpt: SharedObject, forward: String) -> ()
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
#{
    delivery: [
       action "setup forwarding" || forward("john.doe@example.com", "mta-john.example.com"),
    ]
}
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> forward_all </h2>

```rust,ignore
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


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> generate_signature_dkim </h2>

```rust,ignore
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


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> auid </h2>

```rust,ignore
fn get auid(signature: Signature) -> String

```

<details>
<summary markdown="span"> details </summary>

return the `auid` property of the [`Signature`]
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> authid </h2>

```rust,ignore
fn get authid(credentials: Credentials) -> String

```

<details>
<summary markdown="span"> details </summary>

Get the `authid` property of the connection.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> client_address </h2>

```rust,ignore
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


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> client_port </h2>

```rust,ignore
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


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> dkim_result </h2>

```rust,ignore
fn get dkim_result(ctx: Context) -> Map

```

<details>
<summary markdown="span"> details </summary>

Return the DKIM signature verification result in the `ctx()` or
an error if no result is found.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> domains </h2>

```rust,ignore
fn get domains(container: Array) -> Array

```

<details>
<summary markdown="span"> details </summary>

Get the `domains` of an array of email address
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> has_dkim_result </h2>

```rust,ignore
fn get has_dkim_result(ctx: Context) -> bool

```

<details>
<summary markdown="span"> details </summary>

Has the `ctx()` a DKIM signature verification result ?
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> is_authenticated </h2>

```rust,ignore
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


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> local_part </h2>

```rust,ignore
fn get local_part(addr: VSLObject) -> String

```

<details>
<summary markdown="span"> details </summary>

Get the `local part` of an email address
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> mail </h2>

```rust,ignore
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


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> mail_timestamp </h2>

```rust,ignore
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


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> rcpt </h2>

```rust,ignore
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


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> receiver_address </h2>

```rust,ignore
fn get receiver_address(smtp: Smtp) -> String

```

<details>
<summary markdown="span"> details </summary>

Get the receiver address from a smtp service.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> sdid </h2>

```rust,ignore
fn get sdid(signature: Signature) -> String

```

<details>
<summary markdown="span"> details </summary>

return the `sdid` property of the [`Signature`]
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> server_ip </h2>

```rust,ignore
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


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> server_port </h2>

```rust,ignore
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


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> get_all_headers </h2>

```rust,ignore
fn get_all_headers(message: Message) -> Array
fn get_all_headers(message: Message, name: String) -> Array
fn get_all_headers(message: Message, name: SharedObject) -> Array
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


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> get_dmarc_record </h2>

```rust,ignore
fn get_dmarc_record(server: Server, domain: String) -> Record

```

<details>
<summary markdown="span"> details </summary>

Get a valid DMARC record for the domain.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> get_domains </h2>

```rust,ignore
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

```
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


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> get_header </h2>

```rust,ignore
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


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> get_local_part </h2>

```rust,ignore
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

```
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


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> get_private_keys </h2>

```rust,ignore
fn get_private_keys(server: Server, sdid: String) -> Array

```

<details>
<summary markdown="span"> details </summary>

Get the list of DKIM private keys associated with this sdid
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> get_root_domain </h2>

```rust,ignore
fn get_root_domain(domain: String) -> String
fn get_root_domain(domain: SharedObject) -> String
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

<h2 class="func-name"> <code>fn</code> has_expired </h2>

```rust,ignore
fn has_expired(signature: Signature, epsilon: int) -> bool

```

<details>
<summary markdown="span"> details </summary>

Has the signature expired?

return `true` if the argument are invalid (`epsilon` is negative)
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> has_header </h2>

```rust,ignore
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


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> identifier </h2>

```rust,ignore
fn identifier(identifier: String) -> VSLObject

```

<details>
<summary markdown="span"> details </summary>

a user identifier.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> info </h2>

```rust,ignore
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


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> ip6 </h2>

```rust,ignore
fn ip6(ip: String) -> VSLObject

```

<details>
<summary markdown="span"> details </summary>

Build an ip6 address. (x:x:x:x:x:x:x:x)
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> log </h2>

```rust,ignore
fn log(level: String, message: String)
fn log(level: SharedObject, message: SharedObject)
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


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> lookup </h2>

```rust,ignore
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

```
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


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> maildir </h2>

```rust,ignore
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


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> mbox </h2>

```rust,ignore
fn mbox(context: Context, rcpt: SharedObject) -> ()
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


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> msg </h2>

```rust,ignore
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

```
#{
    connect: [
       action "raw message" || msg().rewrite_mail_from_message("john.doe@example.com"),
    ]
}
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> parse_rfc5322_from </h2>

```rust,ignore
fn parse_rfc5322_from(message: Message) -> SharedObject

```

<details>
<summary markdown="span"> details </summary>

Get the address of the sender in the message body, also known as RFC5322.From
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> prepend_header </h2>

```rust,ignore
fn prepend_header(message: Message, header: String, value: String) -> ()
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


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> regex </h2>

```rust,ignore
fn regex(regex: String) -> VSLObject

```

<details>
<summary markdown="span"> details </summary>

a regex (^[a-z0-9.]+@foo.com$)
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> remove_header </h2>

```rust,ignore
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


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> remove_rcpt_envelop </h2>

```rust,ignore
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


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> remove_rcpt_message </h2>

```rust,ignore
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


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> rename_header </h2>

```rust,ignore
fn rename_header(message: Message, old: SharedObject, new: SharedObject) -> ()
fn rename_header(message: Message, old: SharedObject, new: String) -> ()
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


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> rewrite_mail_from_envelop </h2>

```rust,ignore
fn rewrite_mail_from_envelop(context: Context, new_addr: SharedObject) -> ()
fn rewrite_mail_from_envelop(context: Context, new_addr: String) -> ()
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


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> rewrite_mail_from_message </h2>

```rust,ignore
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


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> rewrite_rcpt_envelop </h2>

```rust,ignore
fn rewrite_rcpt_envelop(context: Context, old_addr: SharedObject, new_addr: SharedObject) -> ()
fn rewrite_rcpt_envelop(context: Context, old_addr: String, new_addr: String) -> ()
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
       action "rewrite envelop" || rewrite_rcpt_envelop(address("john.doe@example.com"), address("john.main@example.com")),
    ]
}
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> rewrite_rcpt_message </h2>

```rust,ignore
fn rewrite_rcpt_message(message: Message, old_addr: String, new_addr: SharedObject) -> ()
fn rewrite_rcpt_message(message: Message, old_addr: SharedObject, new_addr: SharedObject) -> ()
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
       action "rewrite recipient" || rewrite_rcpt_message("john.doe@example.com", address("john-mta@example.com")),
    ]
}
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> rg6 </h2>

```rust,ignore
fn rg6(range: String) -> VSLObject

```

<details>
<summary markdown="span"> details </summary>

an ip v6 range. (x:x:x:x:x:x:x:x/range)
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> rlookup </h2>

```rust,ignore
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

```
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
#{
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


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> run </h2>

```rust,ignore
fn run(cmd: Cmd, args: Array) -> Map

```

<details>
<summary markdown="span"> details </summary>

Execute the given command with dynamic arguments.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> set_header </h2>

```rust,ignore
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


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> sign_dkim </h2>

```rust,ignore
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


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> srv </h2>

```rust,ignore
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

```
#{
    connect: [
       action "raw lookup" || srv().lookup("example.com"),
    ]
}
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> time </h2>

```rust,ignore
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

```
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


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> to_debug </h2>

```rust,ignore
fn to_debug(cmd: Cmd) -> String
fn to_debug(this: VSLObject) -> String
fn to_debug(context: Server) -> String
fn to_debug(context: Context) -> String
fn to_debug(status: Status) -> String
fn to_debug(this: OffsetDateTime) -> String
fn to_debug(record: Record) -> String
```

<details>
<summary markdown="span"> details </summary>


</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> to_string </h2>

```rust,ignore
fn to_string(cmd: Cmd) -> String
fn to_string(this: VSLObject) -> String
fn to_string(_: Server) -> String
fn to_string(_: Context) -> String
fn to_string(status: Status) -> String
fn to_string(this: OffsetDateTime) -> String
```

<details>
<summary markdown="span"> details </summary>


</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> user_exist </h2>

```rust,ignore
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

```
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
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> verify_dkim </h2>

```rust,ignore
fn verify_dkim(message: Message, signature: Signature, key: PublicKey) -> ()

```

<details>
<summary markdown="span"> details </summary>

Operate the hashing of the `message`'s headers and body, and compare the result with the
`signature` and `key` data.

# Examples

```
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
```

Changing the header `Subject` will result in a dkim verification failure.

```
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


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> write </h2>

```rust,ignore
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

