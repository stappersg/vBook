# Rules and Actions

Rules and actions are the entry point to filter emails.

## Syntax

`.vsl` files in your rules directory accepts a special syntax: the `rule` and `action` keywords.

### Rule

A `rule` is used to change the transaction state. You can accept and deny a transaction or simply proceed to the next rule using [rule state functions](./../ref/vSL/api/fn::global::rule_state.md). A `rule` is the main primitive for filtering.

```bnf
<rule>      ::= "rule" <rule-name> "||" <expr>
<rule-name> ::= <string>
<expr>      ::= <rhai-expr> ; any valid Rhai expression. Must return a "state".
```
<p class="ann"> A BNF representation of a rule </p>

```rust
// `deny()` is a function that return the `Deny` state.
// Thus, this rule denies any incoming transaction.
rule "deny all transactions" || deny(),

// Rhai expressions can be declared using the above inline syntax,
// or using code blocks, like bellow.
rule "check client ip" || {
    if client_ip() == "192.168.1.254" {
        return faccept();
    } else {
        return next();
    }
},
```
<p class="ann"> Declaring rules </p>

As you can see in the above example, a rule MUST return a "state" (accept, deny, next, etc). Once the rule is executed and a state returned, vSMTP uses it to change the transaction state.

> Rule engine state and effects are listed in the [rule state reference](../ref/vSL/api/fn::global::rule_state.md).

### Action

An `action` is used to execute arbitrary code (logging, saving an email on disk, etc) without changing the transaction state.

```bnf
<action>      ::= "action" <rule-name> "||" <expr>
<action-name> ::= <string>
<expr>        ::= <rhai-expr> ; any valid Rhai expression.
```
<p class="ann"> BNF representation of an action </p>


```rust
// Write the email as json to a "backup" directory.
action "dump to disk" || dump("backup"),

action "log incoming transaction" || {
    // Logging to /var/log/vsmtp.
    log("info", `new transaction: ${helo()} from ${client_ip()}`);
}
```
<p class="ann"> Declaring actions </p>
