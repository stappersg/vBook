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
//! # Envelop
//!
//! The SMTP envelop can be mutated by several function from this module.
//! # Internal
//!
//! A low level api to get access to internal functions of vsl.
//! # Security
//!
//! This module contains multiple security functions that you can use to protect your server.



<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

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


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

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


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

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


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

```rust
fn check_spf(header: ?)
```

<details>
<summary markdown="span"> details </summary>

Check spf record following the Sender Policy Framework (RFC 7208).
A wrapper with the policy set to "strict" by default.
<!-- markdown-link-check-disable-next-line -->
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


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

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


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

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


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

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


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

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


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

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


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

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


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

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


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

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


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

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


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

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


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

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


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

```rust
fn verify_dkim()
```

<details>
<summary markdown="span"> details </summary>

Verify the `DKIM-Signature` header(s) in the mail and produce a `Authentication-Results`.
If this function has already been called once, it will return the result of the previous call.
<!-- markdown-link-check-disable-next-line -->
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


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

```rust
fn verify_dkim_inner(policy: ?)
```

</div>
</br>

