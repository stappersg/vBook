# Basic configuration

## Listen and serve

First of all, create the file [`/etc/vsmtp/vsmtp.vsl`](/get-started/concepts.html#configuration-file) with this content:

```js
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

  config
}
```


The server can now listen and serve SMTP connections.

> If no interface is specified, the server listens on localhost on port 25, 465 and 587. Remote connections are therefore refused.

```sh
$> sudo systemd restart vsmtp
$> telnet 192.168.1.254:25
220 doe-family.com Service ready
554 permanent problems with the remote server
```

> By default, the server will deny any SMTP transaction. We have to define rules to accept connections and filter messages.

## Define filtering logics

We will configure these rules:

- Messages from blacklisted domain will be rejected.
- As Jenny is 11 years old, Jane wants a blind copy of her daughter messages.
- Messages sent to the family must be delivered in MailBox format.

First, let's define all the required objects for John Doe's MTA.

Create the `/etc/vsmtp/rules/objects.vsl` file with the content:

```js
// -- /etc/vsmtp/rules/objects.vsl
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

// A group to manipulate mailboxes.
export const  family_addr = [john, jane, jimmy, jenny];

// Quarantine folders.
export const unknown_quarantine = "doe/bad_user";
export const virus_queue = "doe/virus";

// A user blacklist file.
export const blacklist = file("blacklist.txt", "fqdn");
```

The content of the `blacklist.txt` file is:

```text
# domain-spam.com
# spam-domain.org
# domain-spammers.com
# foobar-spam-pro.org
```

And create the  `/etc/vsmtp/rules/main.vsl` file with the content:

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

```js
// ...

// entry point for our rules.
config.app.vsl.filepath = "/etc/vsmtp/rules/main.vsl";
```

Restart the server to apply the rules.
