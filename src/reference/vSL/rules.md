# Rules and actions

Rules are the entry point to interact with the SMTP traffic at a user level.
Nevertheless specific parameters like timeout, system logging, tls configuration, etc. are set in the configuration files.

## Overall Syntax

Rules and actions are quite similar except that rules must return a vSL rule engine status.
They follow the same syntax :

```c
rule "name" || {
    ... // check stuff
    vsl::accept() // Rule engine status
}
```

```c
action "name" || {
    ... // do stuff
}
```

There is an inline syntax :

```c
action "name" || instruction
rule "name" || instruction
```

Here are some examples:

```c
// Inline rule
rule "test_connect" || if ctx.client_addr == "192.168.1.254" { vsl::next() } else { vsl::deny() }
```

The same rule, including a log:

```c
rule "test_connect" || {
    vsl::log(`Connection from : ${ctx.client_addr}`, my_connection_log);
    if ctx.client_addr == "192.168.1.254" { vsl::next() } else { vsl::deny() }
}
```

&#9998; | String interpolation requires adding ${} to variables.

An action :

```c
action "test_rewrite" || {
    ctx.rewrite_rcpt("johndoe@compagny.com", "john.doe@company.net");
    ctx.remove_rcpt("customer@company.net");
    ctx.add_rcpt("no-reply@company.net");
},
```

A trailing rule:

```c
rule "default" || vsl::deny() 
```

## Rules and vSMTP Stages

Rules are bounded to a vSMTP stage. Stages can be omitted but must appear only once. They are declared in the `main.vsl` file.

```c
//-- main.vsl

obj fqdn "my_company" "mycompany.net"

run_rules!(
  #{
    connect: [ 
        action "log_connect" || vsl::log(`Connection from : ${ctx.client_addr}`, my_connection_log),
        rule "check_connect" || if ctx.client_addr == "192.168.1.254" { vsl::next() } else { vsl::deny() },
    ]
    rcpt: [
        action "rewrite_recipients" || {
            ctx.rewrite_rcpt("johndoe@compagny.com", "john.doe@company.net");
            ctx.remove_rcpt("customer@company.net");
            ctx.add_rcpt("no-reply@company.net");
        },
        rule "local_domain" || {
            rule "test_fqdn" || if my_company in ctx.rcpt.domains { vsl::next() } else { vsl::deny() }
        },
        
        ... // other rules / actions

     ]
  }
)
```

## Implicit rules

To avoid undefined behavior, the implicit action in a stage is `vsl::next()`.
For security purpose end-users should always add a trailing rule at the end of a stage. if not, the implicit next() of the last rule will jump to the next stage.

```c
//-- main.vsl

obj fqdn "my_company" "mycompany.net"

run_rules!(
  #{
    connect: [ 
        rule "test_connect" || if ctx.client_addr == "192.168.1.254" { vsl::next() } else { vsl::deny() },
        action "log_connect" || vsl::log(`Connection from : ${ctx.client_addr}`, my_connection_log),
        // Last action/rule : implicit next() to rcpt stage...
    ]
    rcpt: [
        action "test_rewrite" || {
            ctx.rewrite_rcpt("johndoe@compagny.com", "john.doe@company.net");
            ctx.remove_rcpt("customer@company.net");
            ctx.add_rcpt("no-reply@company.net");
        },
        rule "local_domain" || {
            rule "test_fqdn" || if my_company in ctx.rcpt.domains { vsl::next() } else { vsl::deny() }
        },

        ... // other rules / actions
        
        // Trailing rule (default behavior for rcpt stage)
        rule "default" || vsl::deny() 
     ]
  }
)
```

> As with firewall rules, the best practice is to deny "everything" and only accept authorized and known flows (like the example above).
