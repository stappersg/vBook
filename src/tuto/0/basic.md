# Basic configuration

## The configuration file

`vsmtp.toml` is the main configuration file. It is located in `/etc/vsmtp` directory. Do a backup and open the file with your favorite editor. Remove everything, and copy the configuration bellow.

```toml
# Version requirement. Do not remove or modify it
version_requirement = ">=1.2.1"

# root domain of the server.
[server]
domain = "doe-family.com"

# addresses that the server will listen to.
[server.interfaces]
addr = ["192.168.1.254:25"]
addr_submission = ["192.168.1.254:587"]
addr_submissions = ["192.168.1.254:465"]

# Tls settings.
[server.tls]
security_level = "May"
preempt_cipherlist = false
handshake_timeout = "200ms"
protocol_version = ["TLSv1.2", "TLSv1.3"]
certificate = "/etc/letsencrypt/live/mta.doe-family.com/cert.pem"
private_key = "/etc/letsencrypt/live/mta.doe-family.com/privkey.pem"

[server.smtp.auth]
must_be_authenticated = false
enable_dangerous_mechanism_in_clair = false

# The log level that will be written in syslogs.
[server.logs]
level = [ "warn" ]

# Entry point for our rules.
[app.vsl]
filepath = "/etc/vsmtp/rules/main.vsl"
```

Update the IP addresses, the filenames and the paths. The server is now configured. We have to define rules to filter messages.

## vSL : the vSMTP Scripting Language

The behavior of vSMTP can be defined using a simple but powerful programming language, the vSMTP Scripting Language (vSL). It is based on four main concepts : `rules`, `actions`, `objects` and `services`.

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

### Defining objects

Let's define all the required objects for John Doe's MTA.
Open your favorite editor and create a `objects.vsl` file in the `/etc/vsmtp/rules` directory. Do not forget to update the IP addresses, the domain, etc.

```javascript
// -- objects.vsl
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

```shell
cat blacklist.txt
# domain-spam.com
# spam-domain.org
# domain-spammers.com
# foobar-spam-pro.org
```

## Defining directives (rules and actions)

Let's add some rules in the `main.vsl` file for Doe's family MTA.

- As Jenny is 11 years old, Jane wants a blind copy of her daughter messages.
- Messages sent to the family must be delivered in MailBox format.

```javascript
// -- main.vsl
// Import the object file. The 'doe' prefix is an alias.
import "objects" as doe;

#{
  // the "blacklist" will run once the client sends a "MAIL FROM" command.
  // this is the stage when the sender is known. the sender can be accessed using the `mail_from()` function.
  mail: [
    // Deny any sender with a domain listed in the `blacklist` group.
    rule "blacklist" || if mail_from().domain in doe::blacklist { deny() } else { next() }
  ],

  // This stage is executed every time a "RCPT TO" command is sent by the client. The current recipient can be inspected using the `rcpt()` function.
  rcpt: [
    // automatically set Jane as a BCC if Jenny is part of the recipients.
    action "bcc jenny" || if rcpt() is doe::jenny { bcc(doe::jane) },
  ],

  // The deliver stage is executed just before vsmtp delivers the message. It can be used to setup how vsmtp will deliver the message.
  deliver: [
    action "setup delivery" || {
      // if a recipient is part of the family, we deliver
      // the email locally. Otherwise, we just deliver the email
      // to another server.
      for rcpt in rcpt_list() {
        if rcpt in doe::family_addr { maildir(rcpt) } else { deliver(rcpt) }
      }
    }
  ]
}
```
