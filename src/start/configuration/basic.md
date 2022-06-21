# Basic configuration

Several examples can be found in the [example/config](https://github.com/viridIT/vSMTP/tree/main/examples/) folder.

## The configuration file

`vsmtp.toml` is the main configuration file. It is located in `/etc/vsmtp` directory. Backup the `vsmtp.toml` file. Open it with your favorite editor. Remove everything.
We will build it step-by-step.

```toml
# Version requirement. Do not remove or modify it 
version_requirement = ">=1.0.0"

# Global configuration
[server]
domain = "doe-family.com"         

[server.interfaces]
addr = ["192.168.1.254:25"]
addr_submission = ["192.168.1.254:587"]
addr_submissions = ["192.168.1.254:465"]

[server.tls]
security_level = "May"
protocol_version = ["TLSv1.2", "TLSv1.3"]
certificate = "/etc/vsmtp/certs/certificate.crt"
private_key = "/etc/vsmtp/certs/private.key"
```

TODO: Check app folder 

Quite simple, isn't it ?

Now that the server is configured we need to define the rules to apply to a message. This is the role of vSL.

## vSL : the vSMTP Scripting Language

You are able to define the behavior of vSMTP thanks to a simple but powerful programming language, the vSMTP Scripting Language (vSL). vSL is based on four main concepts : `objects`, `services`, `actions` and `rules`.

`Rules` execute code at different stages of a SMTP transaction and then return a status code to vSMTP, telling the server what to do next (deny or force accept a transaction for example).
`Actions` execute code without influencing the server. Compared to a rule, an action does not return anything.
`Objects` contain variables like mailboxes, ip addresses, domain names etc ...

The `main.vsl` file is the entry point for vSL. By default it is located in the `/etc/vsmtp/rules` directory.

### RHAI and vSL

vSMTP scripting is based on RHAI language. Please consult [The RHAI book] for detailed information about variables, functions, etc.

[The RHAI book]: https://rhai.rs/book/

### Defining objects

Objects are declared through the "object" keyword. The basic syntax is:

```c
object <name> <type> = "<value>";
```

Many types are available. Let's define together all the required objects for John Doe's MTA.
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
# cat blacklist.txt
domain-spam.com
spam-domain.org
domain-spammers.com
foobar-spam-pro.org
```

Done. Now we need to apply some rules on these objects.

## Defining directives (rules and actions)

Rules are the entry point to interact with the SMTP traffic at a user level. They are defined in the `/etc/vsmtp/rules/main.vsl` file. Action don't interact with the transaction. They just trigger functions.

Rules and actions have the same syntax, except the first keyword.

```javascript
rule "name" || {              |       action "name" || {
    ... rule body.            |           ... action body.
}                             |       }
```

Let's add some rules in `the main.vsl` file for Doe's family MTA. 

- Jenny is 11 years old, Jane wants a blind copy of her daughter messages.
- IMAP and Maildir format.

```javascript
// -- main.vsl
// Import the object file. The 'doe' prefix is an alias.
import "objects" as doe;

#{
  mail: [
    // Deny any sender with a domain listed in the `blacklist` group.
    rule "blacklist" || if ctx().mail_from.domain in doe::blacklist { deny() } else { next() }
  ],
   
  rcpt: [
    // automatically set Jane as a BCC if Jenny is part of the recipients.
    action "bcc jenny" || if ctx().rcpt is doe::jenny { bcc(doe::jane) },
  ],

  deliver: [
    action "setup delivery" ||
      // if a recipient is part of the family, we deliver
      // the email locally. Otherwise, we just deliver the email
      // to another server.
      for rcpt in ctx().rcpt_list {
        if rcpt in doe::family_addr { maildir(rcpt) } else { deliver(rcpt) }
      }
  ]
}
```
