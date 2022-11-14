TODO: move rules description to rule tutorial.

# Configuring vSMTP

vSMTP, by default, stores it's configuration in `/etc/vsmtp`. Lets look at how files are organized.

## Overview

A typical vSMTP configuration looks like the following.

```
/etc/vsmtp
┣ vsmtp.vsl
┣ conf.d/
┃     ┣ config.vsl
┃     ┗ *.vsl
┣ domain-available/
┃     ┣ main.vsl
┃     ┣ fallback.vsl
┃     ┣ example.com/
┃     ┃    ┣ config.vsl
┃     ┃    ┣ incoming.vsl
┃     ┃    ┣ outgoing.vsl
┃     ┃    ┗ internal.vsl
┃     ┗ test.com/
┃         ┗ ...
┣ services/
┃     ┣ users-ldap.vsl
┃     ┣ backup-mysql.vsl
┃     ┗ *.vsl
┣ objects/
┃     ┣ net.vsl
┃     ┗ *.vsl
┗ plugins/
      ┣ mysql -> /usr/lib/vsmtp-mysql-plugin.so
      ┗ ldap  -> /usr/lib/vsmtp-ldap-plugin.so
```

Lets break it down step by step, by building a configuration from scratch.

### Root configuration

In `/etc/vsmtp`, by default, the following is created by vSMTP once installed.

```
/etc/vsmtp
┣ vsmtp.vsl
┗ conf.d/
      ┗ config.vsl
```

`vsmtp.vsl` is the mandatory entrypoint for vSMTP, you SHOULD NOT change any of it's content, as maintainers of the program will edit it following new updates.

`conf.d/config.vsl`, on the other hand, is a mandatory configuration file that contains the root configuration for vSMTP that you can edit to change the configuration.

This file must at least contain the following statement:

```rust
fn on_config(config) {
  return config;
}
```

The `on_config` function is called at the startup of vSMTP, and will load the configuration object `config`.

You are free to modify the `config` object to change the configuration.

> TODO: link to config parameters.

For example:
```rust
fn on_config(config) {
  // Change the name of the server.
  config.server.name = "example.com";

  // Specify addresses that the server will listen to.
  config.server.interfaces = #{
    addr: ["192.168.1.254:25"],
    addr_submission: ["192.168.1.254:587"],
    addr_submissions: ["192.168.1.254:465"],
  };

  // Change the folder containing filtering rules.
  config.app.vsl.dirpath = "/etc/vsmtp/domain-available";

  return config;
}
```

#### Recommandations

Rhai exposes a [module API](https://rhai.rs/book/language/modules/index.html), making it possible to split the configuration by theme.

For the above example, it is recommended that configuration files are split this way:
```diff
/etc/vsmtp
 ┣ vsmtp.vsl
 ┗ conf.d/
       ┣ config.vsl
+      ┣ interfaces.vsl
+      ┗ app.vsl
```

with:
```rust
// /etc/vsmtp/conf.d/interfaces.vsl
//
// addresses that the server will listen to.
export const interfaces = #{
  addr: ["192.168.1.254:25"],
  addr_submission: ["192.168.1.254:587"],
  addr_submissions: ["192.168.1.254:465"],
};
```

and:
```rust
// /etc/vsmtp/conf.d/app.vsl
//
// The folder containing filtering rules.
export const rules_dirpath = "/etc/vsmtp/domain-available";
```

Those modules can then be imported in `config.vsl`, resulting in a more cleaner configuration file.

```rust
import "conf.d/interfaces" as i;
import "conf.d/app" as app;

fn on_config(config) {
  config.server.name = "example.com";
  config.server.interfaces = i::interfaces;
  config.app.vsl.dirpath = app::rules_dirpath;

  return config;
}
```

### Filtering

It is possible to filter emails using `.vsl` files for specific domains.

```diff
/etc/vsmtp
  ┣ vsmtp.vsl
  ┣ conf.d/
  ┃     ┣ config.vsl
  ┃     ┣ interfaces.vsl
  ┃     ┗ app.vsl
+ ┗ domain-available/
+         ┣ main.vsl
+         ┗ fallback.vsl
```

For vSMTP to take a rule path into account, you have to change the configuration in `conf.d/config.vsl` like so:
```rust
fn on_config(config) {
  config.app.vsl.dirpath = "/etc/vsmtp/domain-available";
  return config;
}
```

`.vsl` files in your rules directory accepts a special syntax, called `rule` and `action`.

```rust
rule "deny all transactions" || deny(),

action "log incoming transaction" || {
    // Logging to /var/log/vsmtp.
    log("info", `new transaction: ${helo()} from ${client_ip()}`);
}
```

A `rule` is used to change the transaction state. You can `accept`, `faccept`, `deny` a transaction or simply use `next` to go to the next rule.

An `action` is used to execute arbitrary code (logging, saving an email on disk etc ...) without changing the transaction state.

`rule`s and `action`s are executed by transaction `stages`:

* `connect`: After TCP/IP socket has been accepted.
* `helo`: After receiving HELO/EHLO command.
* `authenticate`: After receiving AUTH command.
* `mail`: After receiving MAIL FROM command.
* `rcpt`: After receiving RCPT TO command.
* `preq`: Before writing email on disk.
* `postq`: After writing email on disk & connection closed.
* `delivery`: Right before sending to recipient.

#### Main

The `main.vsl` script at the root of the rule directory ise used

> TODO: add link to rules / actions.

## Listen and serve

First of all, create the file [`/etc/vsmtp/conf.d/config.vsl`](/get-started/concepts.html#configuration-file) with this content:


The server can now listen and serve SMTP connections.

Now, let's define all the required objects for John Doe's MTA. Those objects are used to configure vSMTP and simplify your rules.

Create the `/etc/vsmtp/rules/objects.vsl` file with the content:

```rust
// -- /etc/vsmtp/objects/family.vsl

// IP addresses of the MTA and the internal IP range.
export const local_mta = ip4("192.168.1.254");
export const internal_net = rg4("192.168.0.0/24");

// Doe's family domain name.
export const family_domain = fqdn("doe-family.com");

// Mailboxes.
export const john = address("john.doe@doe-family.com");
export const jane = address("jane.doe@doe-family.com");
export const jimmy = address("jimmy.doe@doe-family.com");
export const jenny = address("jenny.doe@doe-family.com");
export const fridge = address("IOT-fridge@doe-family.com");

export const family_addr = [john, jane, jimmy, jenny];

// Paths for quarantines.
export const unknown_quarantine = "doe/bad_user";
export const virus_queue = "doe/virus";

// A user blacklist file
export const blacklist = file("conf.d/blacklist.txt", "fqdn");
```

The content of the `blacklist.txt` file is:

```text
domain-spam.com
spam-domain.org
domain-spammers.com
foobar-spam-pro.org
```

The content of `/etc/vsmtp` should now look like this.

```diff
/etc/vsmtp/
 ┣ vsmtp.vsl
 ┣ conf.d/
 ┃      ┣ config.vsl
+┃      ┗ blacklist.txt
+┗ objects/
+       ┗ family.vsl
```

> It is recommended to split the configuration into [Rhai modules](https://rhai.rs/book/language/modules/index.html).

> If no interface is specified, the server listens on localhost on port 25, 465 and 587. Remote connections are therefore refused.

```sh
$> sudo systemd restart vsmtp
$> telnet 192.168.1.254:25
220 doe-family.com Service ready
554 permanent problems with the remote server
```

By default, the server will deny any SMTP transaction. We have to define rules to accept connections and filter messages.

## Define filtering logics

We will configure the following rules:

- Messages from blacklisted domain will be rejected.
- As Jenny is 11 years old, Jane wants a blind copy of her daughter messages.
- Messages sent to the family must be delivered in MailBox format.

Now, create the rule filtering configuration, starting off with the `main.vsl` and `fallback.vsl` scripts in the `domain-available` directory.

```diff
/etc/vsmtp/
 ┣ vsmtp.vsl
 ┣ conf.d/
 ┃      ┣ config.vsl
 ┃      ┗ *.vsl
+┣ domain-available/
+┃      ┣ main.vsl
+┃      ┗ fallback.vsl
 ┗ objects/
        ┗ family.vsl
```

The `main.vsl` file is responsible for handling clients that just connected to vSMTP.

```rust
// -- /etc/vsmtp/rules/main.vsl
// Import the object file. The 'doe' prefix is an alias.
import "objects/family" as doe;

#{
  authenticate: [
    rule "auth" || authenticate(),
  ]
}
```

The `fallback.vsl` script is used when your rules do not handle a specific domain to prevent relaying. Since we do not want to handled any sender / recipient domain that is not `doe-family.com` we can simply deny the transaction.

```rust
#{
  rcpt: [
    rule "deny transaction" || deny(),
  ]
}
```

> Note that, if the `fallback.vsl` script is not present in the rule folder, vSMTP loads the previous 'deny transaction' rule by default.

Lets create rules for the `doe-family.com` domain.

```diff
/etc/vsmtp
 ┣ vsmtp.vsl
 ┣ conf.d/
 ┃      ┣ config.vsl
 ┃      ┗ *.vsl
 ┣ domain-available/
 ┃      ┣ main.vsl
 ┃      ┣ fallback.vsl
+┃      ┗ doe-family.com/
+┃         ┣ incoming.vsl
+┃         ┣ outgoing.vsl
+┃         ┗ internal.vsl
┗ objects/
       ┗ family.vsl
```

vSMTP will pickup any `incoming.vsl`, `outgoing.vsl` and `internal.vsl` scripts under a folder with a fqdn name. Those rules will be run following this logic:

- `incoming.vsl` is run when the sender of the domain is not `doe-family.com` and that recipients domains are `doe-family.com`.
- `outgoing.vsl` is run when the sender of the domain is `doe-family.com` and that recipients domains are not `doe-family.com`.
- `internal.vsl` is run when the sender and recipients domains are both  `doe-family.com`.
