# Delegation

Alongside the `rule` and `actions` keyword, vSL exposes another keyword for filtering: `delegate`.

```bnf
<delegation>      ::= "delegate" <smtp-service> <rule-name> "||" <expr>
<delegation-name> ::= <smtp-service>    ; a valid smtp service.
<delegation-name> ::= <string>
<expr>            ::= <rhai-expr>       ; any valid Rhai expression. Must return a "status".
```

<p style="text-align: center;"> <i>A BNF representation of a delegate directive</i> </p>

The `delegate` directive uses a [`smtp` plugin](../ref/plugins/smtp.md) to delegate an email to a third party software:

```js
export const third_party = smtp(#{
    // Send the email to "127.0.0.1:10026" using the SMTP protocol.
    delegator: #{
        address: "127.0.0.1:10026",
        timeout: "60s",
    },
    // Get back the results on "127.0.0.1:10024".
    receiver: "127.0.0.1:10024",
});
```

<p style="text-align: center;"> <i>Declaring a `smtp` service in /etc/vsmtp/services/smtp.vsl</i> </p>

```js
import "services/smtp" as smtp;

delegate smtp::third_party "delegate to third party" || {
    log("info", "delegation results are in!");

    // ...

    return next();
}
```

<p style="text-align: center;"> <i>Declaring a delegation rule with the previously declared smtp service</i> </p>

The `delegate` directives first send the email to the given address, and wait for the results on the `receiver` address.
The body of a `delegate` directive is executed once the email as been received back from the third party software.

A delegation directive MUST return a status, exactly like a `rule`.
The `delegate` keyword can only be used from the `postq` stage and onwards.

> Rule engine status and effects are listed in the API, in the [rule state reference](../ref/vSL/api/fn::global::rule_state.md).
