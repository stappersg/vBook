# global::spf

Implementation of the Sender Policy Framework (SPF), described by RFC 4408. (<https://www.ietf.org/rfc/rfc4408.txt>)


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> check </h2>

```rust,ignore
fn check(header: String) -> Status
fn check(header: String, policy: String) -> Status
```

<details>
<summary markdown="span"> details </summary>

Check spf record following the Sender Policy Framework (RFC 7208).
A wrapper with the policy set to "strict" by default.
see <https://datatracker.ietf.org/doc/html/rfc7208>

# Args

* `header` - "spf" | "auth" | "both" | "none"

# Return
* `deny(code550_7_23 | code550_7_24)` - an error occurred during lookup. (returned even when a softfail is received using the "strict" policy)
* `next()` - the operation succeeded.

# Effective smtp stage

`rcpt` and onwards.

# Errors

* The `header` argument is not valid.

# Note

`spf::check` only checks for the sender's identity, not the `helo` value.

# Examples

```text
#{
    mail: [
       rule "check spf relay" || spf::check(allowed_hosts),
    ]
}

#{
    mail: [
        // if this check succeed, it wil return `next`.
        // if it fails, it might return `deny` with a custom code
        // (X.7.24 or X.7.25 for example)
        //
        // if you want to use the return status, just put the spf::check
        // function on the last line of your rule.
        rule "check spf 1" || {
            log("debug", `running sender policy framework on ${ctx::mail_from()} identity ...`);
            spf::check("spf", "soft")
        },

        // policy is set to "strict" by default.
        rule "check spf 2" || spf::check("both"),
    ],
}
```
</details>

</div>
</br>

<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> check_raw </h2>

```rust,ignore
fn check_raw() -> Map
```

<details>
<summary markdown="span"> details </summary>

WARNING: Low level API, use `spf::check` instead.

Check spf record following the Sender Policy Framework (RFC 7208).
see <https://datatracker.ietf.org/doc/html/rfc7208>

# Return
* `map` - the result of the spf check, contains the `result`, `mechanism` and `problem` keys.

# Effective smtp stage

`rcpt` and onwards.

# Note

`spf::check` only checks for the sender's identity, not the `helo` value.

# Examples

```text
#{
    mail: [
       rule "check spf relay" || {
            const spf = spf::check_raw();

            log("info", `spf results: ${spf.result}, mechanism: ${spf.mechanism}, problem: ${spf.problem}`)
        },
    ]
}
```
</details>

</div>
</br>
