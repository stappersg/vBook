# Rules, actions & delegate

Rules are the entry point to interact with the SMTP traffic at a user level.
Nevertheless specific parameters like timeout, system logging, tls configuration, etc. are set in the configuration files.

## Overall Syntax

Rules and actions are quite similar except that rules must return a vSL rule engine status.
They follow the same syntax :

```js
rule "rule name" || {
    // ... rule body.
    accept() // a rule returns a rule engine status
}
```

```js
action "action name" || {
    // ... action body.
}
```

You can also use the inline syntax below:

```js
action "name" || instruction,
rule "name" || instruction,
```

Here are some rule examples:

```js
// Inline rule that only accepts a client at 192.168.1.254
rule "check connect" || if ctx().client_ip == "192.168.1.254" { next() } else { deny() }
```

The same rule, including a log:

```js
rule "check connect" || {
    log(`Connection from : ${ctx().client_ip}`);
    if ctx().client_ip == "192.168.1.254" { next() } else { deny() }
}
```

&#9998; | You can use [String Interpolation](https://rhai.rs/book/language/strings-chars.html#string-interpolation) to inject variables in strings.

An action :

```js
action "rewrite envelop" || {
    rewrite_rcpt("johndoe@compagny.com", "john.doe@company.net");
    remove_rcpt("customer@company.net");
    add_rcpt("no-reply@company.net");
},
```

A trailing rule:

```js
rule "default" || deny() 
```

&#9998; | This rule is used by default when you do not specify any vsl file in the toml configuration.

The `delegate` directive is different: it also use a smtp service to delegate the email to a third party software:

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

Check out [The delegation guide](../../start/configuration/delegation.md) for an in-depth description of the delegation mechanism.

## Rules and vSMTP Stages

Rules are bound to a vSMTP stage. Stages can be omitted but must appear only once. They are declared in the `main.vsl` file.

```js
// -- objects.vsl

object my_company fqdn = "mycompany.net";

//-- main.vsl

import "objects" as obj;

#{
    connect: [ 
        action "log connect" || log(`Connection from : ${ctx().client_ip}`),
        rule "check connect" || if ctx().client_ip == "192.168.1.254" { next() } else { deny() },
    ],
    rcpt: [
        action "rewrite recipients" || {
            rewrite_rcpt("johndoe@compagny.com", "john.doe@company.net");
            remove_rcpt("customer@company.net");
            add_rcpt("no-reply@company.net");
        },

        rule "local_domain" || {
            if obj::my_company in ctx().rcpt_list.domains { next() } else { deny() }
        },

        // ... other rules & actions
    ],
}
```

## Implicit rules

To avoid undefined behavior, the implicit status in a stage is `next()`.
For security purpose end-users should always add a trailing rule at the end of a stage. if not, the implicit `next()` of the last rule will jump to the next stage.

```js
//-- objects.vsl

object my_company fqdn = "mycompany.net";

//-- main.vsl
import "objects" as obj;

#{
    connect: [ 
        rule "test connect" || if ctx().client_ip == "192.168.1.254" { next() } else { deny() },
        action "log connect" || log(`Connection from : ${ctx().client_ip}`),
    ],
    rcpt: [

        action "rewrite rcpt" || {
            rewrite_rcpt("johndoe@compagny.com", "john.doe@company.net");
            remove_rcpt("customer@company.net");
            add_rcpt("no-reply@company.net");
        },

        rule "local domain" || {
            if obj::my_company in ctx().rcpt_list.domains { accept() } else { next() }
        },

        // ... other rules / actions

        // Trailing rule (denying is the default behavior for rcpt stage)
        rule "default" || deny(),
    ]
}
```

> As with firewall rules, the best practice is to deny "everything" and only accept authorized and known clients (like the example above).
