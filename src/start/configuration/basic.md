# Basic configuration

Several examples can be found in the [example/config](https://github.com/viridIT/vSMTP/tree/main/examples/) folder.

## The configuration file

`vsmtp.toml` is the main configuration file. It is located in `/etc/vsmtp` directory. Backup the `vsmtp.toml` file. Open it with your favorite editor. Remove everything, and copy the configuration bellow.
```toml
# Version requirement. Do not remove or modify it
version_requirement = ">=1.0.0"

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
[server.logs.level]
server = "warn"

# Entry point for our rules.
[app.vsl]
filepath = "/etc/vsmtp/rules/main.vsl"
```

Now that the server is configured, we need to define rules used to filter messages. This is the role of vSL.

## vSL : the vSMTP Scripting Language

You are able to define the behavior of vSMTP thanks to a simple but powerful programming language, the vSMTP Scripting Language (vSL). vSL is based on four main concepts : `rules`, `actions`, `objects` and `services`.

`Rules` execute code at different stages of a SMTP transaction and then return a status code to vSMTP, telling the server what to do next. Using `rules`, you can deny, accept and quarantine incoming messages.

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

`Actions` simply execute code. Compared to a `rule`, an `action` does not return anything, and thus do not influence the state of a transaction.

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

`Objects` contain re-usable fields like mailboxes, ip addresses, domain names, file content etc ...

```js
// object <name> <type> = "<value>";

object example fqdn = "example.com";
object my_address address = "john.doe@example.com";
object whitelist file:address = "/etc/vsmtp/whitelist.txt";

print(`the example domain: ${example}`);
print(`my personal address: ${my_address}`);
print(`content of whitelist: ${whitelist}`);
```

`Services` are interfaces with third party software.

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

vSMTP scripting is based on the RHAI language. Please consult [The RHAI book] for detailed information about variables, functions, etc.

[The RHAI book]: https://rhai.rs/book/

### Defining objects

Let's define together all the required objects for John Doe's MTA.
Open your favorite editor and create a `objects.vsl` file in the rule directory.

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

Now we need to apply some rules on these objects.

## Defining directives (rules and actions)

Let's add some rules in the `main.vsl` file for Doe's family MTA.
Here is what we want to configure:

- Jenny is 11 years old, Jane wants a blind copy of her daughter messages.
- We want to deliver emails using the Maildir format if a recipient is from the family.

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
      for rcpt in ctx().rcpt_list {
        if rcpt in doe::family_addr { maildir(rcpt.to_string()) } else { deliver(rcpt.to_string()) }
      }
    }
  ]
}
```
