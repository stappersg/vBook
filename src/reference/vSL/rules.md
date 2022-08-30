# Rules, actions & delegate

Rules are the entry point to interact with the SMTP traffic at a user level.

## Overall Syntax

Rules and actions are quite similar but rules must return a vSL rule engine status. They are defined in the same way:

```js
action "action name" || {
    // ... action body.
}
```

```js
rule "rule name" || {
    // ... rule body.
    accept() // a rule returns a rule engine status

}
```

> Rule engine status and effects are listed in the API, in the [status module](api/Status.md).

An inline syntax is also available, like below:

```js
action "name" || instruction,
rule "name" || instruction,
```

An example of a rule:

```js
// Inline rule that only accepts a client at 192.168.1.254
rule "check connect" || if client_ip() == "192.168.1.254" { next() } else { deny() }
```

The same rule, including a [string interpolation](https://rhai.rs/book/language/strings-chars.html#string-interpolation) in a log:

```js
rule "check connect" || {
    log("warn", `Connection from : ${client_ip()}`);
    if client_ip() == "192.168.1.254" { next() } else { deny() }
}
```

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

## Rules and vSMTP Stages

Rules are bound to a vSMTP stage. Stages that are not used can be omitted, but must appear only once if used. They are declared in the `main.vsl` file.

```js
// -- objects.vsl

object my_company fqdn = "mycompany.net";

//-- main.vsl

import "objects" as obj;

#{
    connect: [
        action "log connect" || log("warn", `Connection from : ${client_ip()}`),
        rule "check connect" || if client_ip() == "192.168.1.254" { next() } else { deny() },
    ],

    rcpt: [
        rule "local_domain" || {
            if obj::my_company == rcpt().domain { next() } else { deny() }
        },
    ],

    preq: [
        action "rewrite recipients" || {
            rewrite_rcpt("johndoe@compagny.com", "john.doe@company.net");
            remove_rcpt("customer@company.net");
            add_rcpt("no-reply@company.net");
        },
    ],

    // ... other rules & actions
}
```

## Implicit rules

For security purpose, end-users should always add a trailing rule at the end of a stage. However, to avoid undefined behavior, an implicit trailing rule is set to `next()`, moving the rule engine to the next stage.

```js
//-- objects.vsl

object my_company fqdn = "mycompany.net";

//-- main.vsl
import "objects" as obj;

#{
    rcpt: [
        rule "local domain" || {
            if obj::my_company == rcpt().domain { accept() } else { next() }
        },

        // ... other rules / actions

        // Trailing rule (denying is the default behavior for rcpt stage)
        rule "default" || deny(),
    ]
}
```

> As with firewall rules, the best practice is to deny "everything" and only accept authorized and known clients (like the example above).

## Action

`Actions` are similar to `rules` but do not return any status code and thus cannot modify the state of a transaction.

```js
// action "<name>" || {
//     // <action body>
// }

action "log incoming transaction" || {
  // We use actions to execute code that does not
  // need to change the state of the transaction.
  log("debug", `new transaction by ${client_ip()}`);
}
```
