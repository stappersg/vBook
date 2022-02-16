# Rules and actions

Rules are the entry point to interact with the SMTP traffic at a user level.
Nevertheless specific parameters like timeout, system logging, tls configuration, etc. are set in the configuration files.

## Overall Syntax

Rules and actions are quite similar except that rules must return a vsl rule engine action.
They follow the same syntax :

```rust,ignore
rule "name" || {
    ... // do stuff
    vsl::accept() // Rule engine action
}
```

```rust,ignore
action "name" || {
    ... // do stuff
}
```

There is an inline syntax :

```rust,ignore
rule/action "name" || instruction,
```

Here are some examples:


An inline rule :

```rust,ignore
rule "test_connect" || if ctx.client_addr == "192.168.1.254" { vsl::next() } else { vsl::deny() }
```

The same rule, including a log:

```rust,ignore
rule "test_connect" || {
      vsl::log(`Connection from : ${ctx.client_addr}`, my_connexion_log);
      if ctx.client_addr == "192.168.1.254" { vsl::next() } else { vsl::deny() }
    }
```

&#9998; | String interpolation requires adding ${} to variables.

An action :

```rust,ignore
action "test_rewrite" || {
        ctx.rewrite_rcpt("johndoe@compagny.com", "john.doe@company.net");
        ctx.remove_rcpt("customer@company.net");
        ctx.add_rcpt("no-reply@company.net");
      },
```

A trailing rule:

```rust,ignore
rule "default" || vsl::deny() 
```


## Structure


obj ident "john" "johndoe";
obj fqdn "viridit" "viridit.com";
obj addr "customer" "customer@company.com";

```rust,ignore



run_rules!(     # This is the main part
  #{
    connect: [ ]
    helo: [ ]
    mail: [ ]
    rcpt: [ ]
    preq: [ ]
    postq: [ ]
  }
)





### Conditions

The "condition: ||" primitive expects a boolean after the || symbol.
Booleans can come directly from [RHAI](https://rhai.rs/) or vSL functions as shown hereunder (like vsl.IS_CONNECT).

#### Built-in vSL conditions

Foreach stage a vSL condition that match the message context is available.
The function syntax is : IS_*STAGE*(object).

```rust,ignore
obj ip4 "localhost" "192.168.1.34";

rule connect "check on connect" #{
    condition:  || vsl.IS_CONNECT("localhost"),
    on_success: || vsl.ACCEPT(),
    on_failure: || vsl.DENY()
};
```

As explained previously, the values obtained from the previous steps are still available in the current stage.

```rust,ignore
obj ip4 "localhost" "192.168.1.34";
obj addr "foo" "foo@bar.com";

rule mail "adv check" #{
    condition:  || vsl.IS_CONNECT("localhost") && vsl.IS_MAIL("foo"),
    on_success: || vsl.ACCEPT(),
    on_failure: || vsl.DENY()
};
```

#### Complex conditions using [RHAI](https://rhai.rs/) functions

```rust,ignore
obj fqdn "foobar" "my.foo.bar";

fn my_function(x) {
    if (x == "foo") { true } else { false }
}

[...]
rule mail "adv check" #{
    condition: || !vsl.IS_HELO("foobar") && my_function("bar"),
[...]
```

&#9758; | The operators && and || are short-circuits. In this case my_function() function will not be evaluated if the 1st part already proves the condition wrong. To counter this behavior use the boolean operators & and |.

### Rule actions : on_success and on_failure

These methods interact with the SMTP engine.
Those methods must return a state (see the Rule Engine Actions section) to influence vSMTP.

for example:

```rust,ignore
obj ip4 "localhost" "192.168.1.34";

fn my_action() {
    vsl.DUMP(`/tmp/mail/dump/${msg_id}`);
    vsl.FACCEPT()
}

rule connect "check on connect" #{
    condition:  || vsl.IS_CONNECT("localhost"),
    on_success: || my_action(),
    on_failure: || {
        vsl.LOG(`Connection from this host is not allowed.`, "stdout");
        vsl.DENY()
    },
};
```

The connection is accepted if it is local, and denied otherwise.

&#9998; | The absence of the semicolon after DENY() since the rule must return a state.

### Implicit rule in a stage

To avoid undefined behavior, the implicit action in a stage is CONTINUE(). If there's no state (i.e.  ACCEPT, DENY, etc.) returned in a stage, the default behavior is to proceed to the next stage, and in the end the message is delivered.

### About DUMP action

The DUMP action writes the content of an email in JSON format with the content available at the specified rule stage.

```rust,ignore
rule mail "dump_at_mail_stage" #{
    condition: true,
    on_success: vsl.DUMP(`/var/spool/mta/`),
};
```

This rule will dump in JSON format only the content available at the "mail" stage : `connect`, `helo` and `mail` parameters.

### About BLOCK action

The BLOCK action pushes the mail in a user defined quarantine directory.
Unlike DUMP:

- The ENTIRE content of the email is written in JSON format regardless of the stage declared in the rule (including the envelop and body).
- All rules are skipped, and the server delivers a 554 smtp code to the client.

```rust,ignore
rule helo "my_quarantine" #{
    condition: vsl.IS_HELO("blacklist"),
    on_success: || vsl.BLOCK("/var/spool/mta/blacklist/"),
    ...
};
```
