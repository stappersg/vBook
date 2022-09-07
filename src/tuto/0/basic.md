# Basic configuration

## Listen and serve

First of all, create the file [`/etc/vsmtp/vsmtp.toml`](/get-started/concepts.html#configuration-file) with this content:

```toml
version_requirement = ">=1.3.0"

# root domain of the server.
[server]
domain = "doe-family.com"

# addresses that the server will listen to.
# (change `192.168.1.254` for the address you want to listen to)
[server.interfaces]
addr = ["192.168.1.254:25"]
addr_submission = ["192.168.1.254:587"]
addr_submissions = ["192.168.1.254:465"]
```

Your server can now listen and serve.

```sh
$> sudo systemd restart vsmtp
$> telnet 192.168.1.254:25
220 doe-family.com Service ready
554 permanent problems with the remote server
```

By default, the server will deny any connection. We have to define rules to process the connection and filter messages.

## Define filtering logics

We will configure these rule:

- Messages from blacklisted domain will be rejected.
- As Jenny is 11 years old, Jane wants a blind copy of her daughter messages.
- Messages sent to the family must be delivered in MailBox format.

First, let's define all the required objects for John Doe's MTA.

Create the file `/etc/vsmtp/rules/objects.vsl` with the content:

```js
// -- /etc/vsmtp/rules/objects.vsl
// IP addresses of the MTA and the internal IP range.
object local_mta ip4 = "192.168.1.254";
object internal_net rg4 = "192.168.0.0/24";

// Doe's family domain name.
object family_domain fqdn = "doe-family.com";

// Mailboxes.
object john address = "john.doe@doe-family.com";
object jane address = "jane.doe@doe-family.com";
object jimmy address = "jimmy.doe@doe-family.com";
object jenny address = "jenny.doe@doe-family.com";

// A group to manipulate mailboxes.
object family_addr group = [john, jane, jimmy, jenny];

// Quarantine folders.
object unknown_quarantine string = "doe/bad_user";
object virus_queue string = "doe/virus";

// A user blacklist file.
object blacklist file:fqdn = "blacklist.txt";
```

The content of the `blacklist.txt` file is:

```text
# domain-spam.com
# spam-domain.org
# domain-spammers.com
# foobar-spam-pro.org
```

And create the file `/etc/vsmtp/rules/main.vsl` with the content:

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

  // The deliver stage is executed just before vsmtp delivers the message.
  deliver: [
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

Add these lines to your `/etc/vsmtp/vsmtp.toml`:

```toml
# ...

# entry point for our rules.
[app.vsl]
filepath = "/etc/vsmtp/rules/main.vsl"
```

Fantastic ! You can restart your server to apply the new rules, but our server need security policies.
