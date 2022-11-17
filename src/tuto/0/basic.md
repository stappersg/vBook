# Basic configuration

## vSMTP Configuration

Let's build a vSMTP configuration step by step. For a full description of the configuration file hierarchy, read the [Configuring vSMTP](./../../get-started/config-file-struct.md) chapter.

When installing vSMTP, the package manager should create the following basic configuration.

```diff
/etc/vsmtp
+┣ vsmtp.vsl
+┗ conf.d/
+      ┗ config.vsl
```

> For more details on root configuration files, check out the [`Configuring vSMTP`](/src/get-started/config-file-struct.md###root-configuration) chapter.

## Listen and serve

First of all, modify the [`/etc/vsmtp/conf.d/config.vsl`](/src/get-started/config-file-struct.md###root-configuration) file with this configuration:

```rust
fn on_config(config) {
  // Name of the server.
  config.server.name = "doe-family.com";

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

> To get an exhaustive list of parameters that you can change in the configuration, see the [Configuration Reference](TODO:) chapter.

The server can now listen and serve SMTP connections.

Now, let's define all the required objects for John Doe's MTA. Those objects are used to configure vSMTP and simplify your rules.

Create the `/etc/vsmtp/rules/objects.vsl` file with following objects:

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

> See the [Object Reference](/src/reference/vSL/objects.md#Objects) chapter for more information.

The contents of the `/etc/vsmtp/conf.d/blacklist.txt` file is:

```text
domain-spam.com
spam-domain.org
domain-spammers.com
foobar-spam-pro.org
```

The file structure of `/etc/vsmtp` should now look like this.

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

Now, restart vSMTP and open a connexion on port 25.

```sh
$> sudo systemd restart vsmtp
$> telnet 192.168.1.254:25
220 doe-family.com Service ready
554 permanent problems with the remote server
```

By default, the server will deny any SMTP transaction. We have to define [filtering rules](/src/reference/vSL/rules.md) to accept connections and filter messages.

## Define filtering logics

We will configure the following rules:

- Messages from blacklisted domain will be rejected.
- As Jenny is 11 years old, Jane wants a blind copy of her daughter messages.
- Messages sent to the family must be delivered in MailBox format.

Create the rule filtering configuration, starting off with the root `incoming.vsl` script in the `domain-available` directory. In the [`Listen and serve`](##listen-and-serve) section, we defined `/etc/vsmtp/domain-available` as the rule folder.

```diff
/etc/vsmtp/
 ┣ vsmtp.vsl
 ┣ conf.d/
 ┃      ┣ config.vsl
 ┃      ┗ *.vsl
+┣ domain-available/
+┃      ┗ incoming.vsl
 ┗ objects/
        ┗ family.vsl
```

The `incoming.vsl` file is responsible for handling clients that just connected to vSMTP.

```rust
// -- /etc/vsmtp/domain-available/incoming.vsl
#{
  // Ask the client to authenticate.
  authenticate: [
    rule "auth" || authenticate(),
  ]
}
```

> To create your own filtering rules, check out the following chapters:
> * [The Rule reference](/src/reference/vSL/rules.md)
> * [The Stage reference](/src/reference/vSL/stages.md)
> * [Transaction context](/src/reference/vSL/transaction.md)

Anti-relaying can be achieved by adding the following rule to your root `incoming.vsl` script. (See the [Root Incoming](/src/reference/vSL/transaction.md##root-incoming) section in the [Transaction Context](/src/reference/vSL/transaction.md) chapter)

```rust
#{
  rcpt: [
    rule "anti relaying" || deny(),
  ]
}
```

Let's create filtering rules for the `doe-family.com` domain.

```diff
/etc/vsmtp
 ┣ vsmtp.vsl
 ┣ conf.d/
 ┃      ┣ config.vsl
 ┃      ┗ *.vsl
 ┣ domain-available/
 ┃      ┣ incoming.vsl
+┃      ┗ doe-family.com/
+┃         ┣ incoming.vsl
+┃         ┣ outgoing.vsl
+┃         ┗ internal.vsl
┗ objects/
       ┗ family.vsl
```

vSMTP will pickup any `incoming.vsl`, `outgoing.vsl` and `internal.vsl` scripts under a folder with a fully qualified domain name. Those rules will be run following [this logic](/src/reference/vSL/transaction.md):

- `doe-family.com/incoming.vsl` is run when the sender of the domain is not `doe-family.com` and that recipients domains are `doe-family.com`.
- `doe-family.com/outgoing.vsl` is run when the sender of the domain is `doe-family.com` and that recipients domains are not `doe-family.com`.
- `doe-family.com/internal.vsl` is run when the sender and recipients domains are both  `doe-family.com`.

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
