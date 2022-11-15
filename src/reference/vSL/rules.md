# Rules, actions & delegate

Rules are the entry point to filter emails.

## Syntax

`.vsl` files in your rules directory accepts a special syntax: the `rule` and `action` keywords.

### Rule

A `rule` is used to change the transaction state. You can `accept`, `faccept`, `deny` a transaction or simply use `next` to go to the next rule. This is the main primitive for filtering.

A BNF representation of a rule.
```bnf
<rule>      ::= "rule" <rule-name> "||" <rhai-expr>
<rule-name> ::= <string>
<expr>      ::= <rhai-expr> ; any valid Rhai expression. Must return a "status".
```

An example of a rule declaration in practice.
```rust
// `deny()` is a function that return the `Deny` status.
// Thus, this rule denies any incoming transaction.
rule "deny all transactions" || deny(),

// Rhai expressions can be declared using the above inline syntax,
// or using code blocks, like bellow.
rule "check client ip" || {
    if client_ip() == "192.168.1.254" {
        faccept()
    } else {
        next()
    }
},
```

> Rule engine status and effects are listed in the API, in the [status module](api/Status.md).

### Action

An `action` is used to execute arbitrary code (logging, saving an email on disk etc ...) without changing the transaction state.

A BNF representation of an action.
```bnf
<action>      ::= "action" <rule-name> "||" <rhai-expr>
<action-name> ::= <string>
<expr>        ::= <rhai-expr> ; any valid Rhai expression.
```

An example of an action declaration in practice.
```rust
action "dump to disk" || dump("backup"),

action "log incoming transaction" || {
    // Logging to /var/log/vsmtp.
    log("info", `new transaction: ${helo()} from ${client_ip()}`);
}
```

### Delegate

TODO: update delegation docs.

The `delegate` directive is different: it uses a smtp service to delegate the email to a third party software:

```js
service third_party smtp = #{
    delegator: #{
        address: "127.0.0.1:10026",
        timeout: "60s",
    },
    receiver: "127.0.0.1:10024",
};

delegate third_party "delegate email processing" || { ... }
```

Check out the [Policy delegation](../../start/configuration/delegation.md) chapter for an in-depth description of the delegation mechanism.

## Using them

Rules and actions are grouped by `stages`. Those are covered in the next chapter: [Stages](stages.md).