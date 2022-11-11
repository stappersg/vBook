# Basic configuration

## vSMTP Configuration

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

Lets build a vSMTP configuration step by step, starting with the root configuration.

In `/etc/vsmtp`, create the following files.

```diff
/etc/vsmtp
+┣ vsmtp.vsl
+┗ conf.d/
+      ┗ config.vsl
```

`vsmtp.vsl` is the root configuration file for vSMTP, you should not change any of it's content.
`conf.d/config.vsl` is a mandatory configuration file that contains the root configuration for vSMTP.

This file must at least contain the following statement:

```rust
// vSMTP calls this function once it starts, and lets you configure the server
// with the `config` parameter.
fn on_config(config) {
  // We return the config object.
  config
}
```

the `on_config` function is called at the startup of vSMTP, and will load the configuration object `config`.

## Listen and serve

First of all, create the file [`/etc/vsmtp/conf.d/config.vsl`](/get-started/concepts.html#configuration-file) with this content:

```rust
fn on_config(config) {
  // root domain of the server.
  config.server.domain = "doe-family.com";

  // addresses that the server will listen to.
  // (change `192.168.1.254` for the address you want to listen to)
  config.server.interfaces = #{
    addr: ["192.168.1.254:25"],
    addr_submission: ["192.168.1.254:587"],
    addr_submissions: ["192.168.1.254:465"],
  };

  // The folder containing filtering rules.
  config.app.vsl.dirpath = "/etc/vsmtp/domain-available";

  config
}
```

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

# TODO: remove

```js
// -- /etc/vsmtp/rules/main.vsl
// Import the object file. The 'doe' prefix is an alias.
import "objects" as doe;

#{
  // List of rules execute after receiving "MAIL FROM" from a client.
  // At this stage the sender is known and can be accessed using `mail_from()`.
  mail: [
    // Deny any sender with a domain listed in the `blacklist` group.
    rule "blacklist" || {
      if mail_from().domain in doe::blacklist { deny() } else { next() }
    }
  ],

  // List of rules execute after receiving "RCPT TO" from a client.
  // The current recipient can be inspected using `rcpt()`.
  rcpt: [
    // automatically set Jane as a BCC if Jenny is part of the recipients.
    action "bcc jenny" || if rcpt() is doe::jenny { bcc(doe::jane) },
  ],

  // The delivery stage is executed just before vsmtp delivers the message.
  delivery: [
    action "setup delivery" || {
      // if a recipient is part of the family, we deliver the email locally.
      // Otherwise, we just deliver the email to another server.
      for rcpt in rcpt_list() {
        if rcpt in doe::family_addr { maildir(rcpt) } else { deliver(rcpt) }
      }
    }
  ]
}
```

Add these lines to your `/etc/vsmtp/vsmtp.vsl`:

Restart the server to apply the rules.
