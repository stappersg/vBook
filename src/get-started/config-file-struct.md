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
┃     ┣ incoming.vsl
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
      ┣ mysql -> /usr/lib/vsmtp/vsmtp-mysql-plugin.so
      ┗ ldap  -> /usr/lib/vsmtp/vsmtp-ldap-plugin.so
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
+         ┗ incoming.vsl
```

For vSMTP to take a rule path into account, you have to change the configuration in `conf.d/config.vsl` like so:
```rust
fn on_config(config) {
  config.app.vsl.dirpath = "/etc/vsmtp/domain-available";
  return config;
}
```

#### Main

The `main.vsl` script is used to filter incoming transaction at the `connect`, `helo` and `authenticate` stages.

> TODO: add link to rules / actions.

#### incoming

The root `incoming.vsl` script is run when an incoming sender domain is not handled by the configuration. If this file is not present in the rule directory, it will deny any incoming relaying tentative by clients.

> TODO: add link to rules / actions.

#### Sub domains

In the rule directory, any subfolder is considered as a subdomain that vSMTP handles.

For example:
```diff
/etc/vsmtp
  ┣ vsmtp.vsl
  ┣ conf.d/
  ┃     ┣ config.vsl
  ┃     ┣ interfaces.vsl
  ┃     ┗ app.vsl
  ┗ domain-available/
          ┣ main.vsl
          ┣ incoming.vsl
+         ┗ example.com
+             ┣ incoming.vsl
+             ┣ outgoing.vsl
+             ┗ internal.vsl
```

Here, an `example.com` folder has been added. vSMTP will pickup the scripts defined in this folder and run them following the following conditions.

##### Incoming

The `incoming.vsl` script is run if the sender domain is not handled by the configuration, but domains from recipients are.

Thus:
```sh
MAIL FROM: <john.doe@unknown.com> # We don't have a `unknown.com` folder, this is an incoming message.
RCPT TO:   <foo@example.com>      # `example.com` is handled, we run `incoming.vsl`.
RCPT TO:   <bar@example.com>      # Same as above.
```

If any recipient domain in this context is not handled by the configuration, then the root `incoming.vsl` is called instead.

Thus:
```sh
MAIL FROM: <john.doe@unknown.com> # We don't have a `unknown.com` folder, this is an incoming message.
RCPT TO:   <foo@example.com>      # `example.com` is handled, we run `incoming.vsl` in the `example.com` folder.
RCPT TO:   <bar@anonymous.com>    # We don't have a `unknown.com` folder, root `incoming.vsl` is used.
```

A client should not mix up multiple recipient domains when sending a message to the server. This is why the root script is called when this happens. Once again, if the root `incoming.vsl` is not defined, the transaction will be denied by default.

##### Outgoing

The `outgoing.vsl` script is run if the sender domain is handled by the configuration, but recipients are not.

Thus:
```sh
MAIL FROM: <john.doe@example.com> # `example.com` exists, this is an outgoing message.
RCPT TO:   <foo@anonymous.com>    # We don't have a `anonymous.com` folder, `outgoing.vsl` is used.
RCPT TO:   <bar@anonymous.com>    # Same as above.
```

##### Internal

The `internal.vsl` script is run if the sender and recipients domains are handled by the configuration and the exact same.

Thus:
```sh
MAIL FROM: <john.doe@example.com> # `example.com` exists, we don't know yet about the recipient, so this is an outgoing message.
RCPT TO:   <foo@example.com>    # The domain is the same as the sender, `internal.vsl` is used.
RCPT TO:   <bar@example.com>    # Same as above.
```

#### Sub domain specific configuration

It is possible to add a specific configuration for each sub domain. 

```diff
/etc/vsmtp
  ┣ vsmtp.vsl
  ┣ conf.d/
  ┃     ┣ config.vsl
  ┃     ┣ interfaces.vsl
  ┃     ┗ app.vsl
  ┗ domain-available/
          ┣ main.vsl
          ┣ incoming.vsl
          ┗ example.com
+             ┣ config.vsl
              ┣ incoming.vsl
              ┣ outgoing.vsl
              ┗ internal.vsl
```

The `config.vsl` under a sub domain must contain the following statement:

```rust
fn on_domain_config(config) {
  config
}
```

As the root `config.vsl` file, this script contains a callback used to configure the sub domain. You can configure TLS, DKIM and DNS per sub-domain.

For example:
```rust
fn on_domain_config(config) {
  config.tls = #{
    protocol_version: ["TLSv1.2", "TLSv1.3"],
    certificate: "/etc/vsmtp/certs/cert.pem",
    private_key: "/etc/vsmtp/certs/privkey.pem",
  };

  config.dkim = #{
    private_key: "/etc/vsmtp/certs/example.dkim.key",
  };

  config.server.dns.type = "system";

  config
}
```

If this script is not present in a subdomain, configuration from the root `config.vsl` script is used instead.

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

Now, create the rule filtering configuration, starting off with the `main.vsl` and `incoming.vsl` scripts in the `domain-available` directory.

```diff
/etc/vsmtp/
 ┣ vsmtp.vsl
 ┣ conf.d/
 ┃      ┣ config.vsl
 ┃      ┗ *.vsl
+┣ domain-available/
+┃      ┣ main.vsl
+┃      ┗ incoming.vsl
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

The root `incoming.vsl` script is used when your rules do not handle a specific domain to prevent relaying. Since we do not want to handle any sender / recipient domain that is not `doe-family.com` we can simply deny the transaction.

```rust
#{
  rcpt: [
    rule "deny transaction" || deny(),
  ]
}
```

> Note that, if the root `incoming.vsl` script is not present in the rule folder, vSMTP loads the previous 'deny transaction' rule by default.

Lets create rules for the `doe-family.com` domain.

```diff
/etc/vsmtp
 ┣ vsmtp.vsl
 ┣ conf.d/
 ┃      ┣ config.vsl
 ┃      ┗ *.vsl
 ┣ domain-available/
 ┃      ┣ main.vsl
 ┃      ┣ incoming.vsl
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
