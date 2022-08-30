# vSL - the vSMTP Scripting Language

vSL is a lightweight scripting language dedicated to email filtering. It is based on the [Rhai](https://rhai.rs) scripting language.

The entry point for vSMTP is a file defined in the [configuration file](/reference/config-file.html#appvsl) (`/etc/vsmtp/rules/main.vsl` usually). This file must be evaluated as a [Rhai map](https://rhai.rs/book/language/object-maps.html#object-maps), composed of keys and values.

* Keys are [transaction stages](/reference/vSL/stages.html)
* Values are arrays of [rule](/reference/vSL/rules.html), [action](/reference/vSL/rules.html#action) or [delegate](/tuto/0/antivirus.html#the-delegate-keyword) which will be executed at the corresponding stage.

To avoid repetitive code in your logics, you can define [objects](objects.md), use the [vsl api](api.md) and use dedicated [services](services.md) to interact with third-party software.

A `/etc/vsmtp/rules/main.vsl` file can grow large is you define a lot of logics, but you can split all your `.vsl` in severals files using [Rhai modules](https://rhai.rs/book/ref/modules/index.html).

> Store all you `.vsl` files in the `/etc/vsmtp/rules` folder and use a version control system such as [git](https://git-scm.com/).

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

> Syntax highlighting is available for Microsoft [VSCode](https://code.visualstudio.com/) IDE, using the [Rhai extension](https://marketplace.visualstudio.com/items?itemName=rhaiscript.vscode-rhai).
