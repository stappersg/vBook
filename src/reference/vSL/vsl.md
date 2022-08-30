# vSL - the vSMTP Scripting Language

vSL is a lightweight scripting language dedicated to email filtering. It is based on the [Rhai] scripting language.

> Code highlighting is available for Microsoft [VSCode](https://code.visualstudio.com/) IDE, using the [Rhai extension](https://marketplace.visualstudio.com/items?itemName=rhaiscript.vscode-rhai).

[Rhai]: https://rhai.rs/

To interact with the SMTP traffic, vSL combines:

- filtering [rules].
- Configuration-like [objects]
- email utilities wrapped in [functions].
- [services] to interact with third-party software

[rules]: rules.md
[objects]: objects.md
[functions]: api.md
[services]: services.md

Rules can be applied at any [stage] of the SMTP transaction.

[stage]: stages.md

The [delivery] system uses the same concepts by applying rules to targeted domains and users.

[delivery]: delivery.md

These sections describe the gist of how the rule system works. Advanced user can use the [Rhai] scripting language on top of vSL to create and manage a wide variety of actions.

### TODO

<!--
The `main.vsl` file in the `/etc/vsmtp/rules` folder is the entry point for the rules engine.
The `.vsl` files are commonly stored in the `/etc/vsmtp/rules` directory.
-->

`Rules` may be defined at each step of a SMTP transaction. They return a status code requesting the vSMTP server to deny, accept or quarantine a message.

```js
// rule "<name>" || {
//     // <rule body>
//     return <status-code>;
// }

rule "my blacklist" || {
  if client_ip() == "222.11.16.196" {
    // Spam address detected ! We deny the transaction.
    deny()
  } else {
    // the client ip is valid, we can proceed.
    next()
  }
}
```

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

`Objects` are typed containers like mailboxes, ip addresses, domain names, file content, etc.

```js
// object <name> <type> = "<value>";

object example fqdn = "example.com";
object my_address address = "john.doe@example.com";
object whitelist file:address = "/etc/vsmtp/whitelist.txt";

print(`the example domain: ${example}`);
print(`my personal address: ${my_address}`);
print(`content of whitelist: ${whitelist}`);
```

`Services` define interfaces with third party software.

```js
// service <name> <type>[:<content-type>] = "<value>";

// vsmtp will send messages using the smtp protocol
// to the software listening on 127.0.0.1:10026.
service clamsmtpd smtp = #{
    delegator: #{
        address: "127.0.0.1:10026",
        timeout: "60s",
    },
    receiver: "127.0.0.1:10024",
};

// vsmtp will connect to a csv database with
// this service.
service greylist db:csv = #{
    connector: "/db/user_accounts.csv",
    access: "O_RDONLY",
    refresh: "always",
    delimiter: ",",
};
```

The `main.vsl` file is the entry point for vSL, located in the `/etc/vsmtp/rules` directory by default.

### RHAI and vSL

vSMTP scripting is based on the RHAI language. Please consult [The RHAI book] for detailed information.

[The RHAI book]: https://rhai.rs/book/
