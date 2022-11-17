# vSL - the vSMTP Scripting Language

vSL is a lightweight scripting language dedicated to email filtering. It is based on the fully featured [Rhai](https://rhai.rs) scripting language. To make the most out of vSL, it is recommended that you read Rhai's documentation.

vSL, on top of Rhai, adds:
* Functions used to query vSMTP on the current transaction's data.
* Constructors used to create objects like regex, fqdn and addresses for filtering.
* Services, objects that helps vSMTP to interact with third party software.
* A special `rule` syntax to filter emails.

> Syntax highlighting is available for Microsoft [VSCode](https://code.visualstudio.com/) IDE, using the [Rhai extension](https://marketplace.visualstudio.com/items?itemName=rhaiscript.vscode-rhai).

<!--
### TODO

The [delivery](delivery.md) system uses the same concepts by applying rules to targeted domains and users.

These sections describe the gist of how the rule system works. Advanced user can use the [Rhai] scripting language on top of vSL to create and manage a wide variety of actions.

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
-->