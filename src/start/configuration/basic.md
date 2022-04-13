# Basic configuration

## The configuration file

`vsmtp.toml` is the main configuration file. It is located in `/etc/vsmtp` directory. Examples can be found in vSMTP repository in the [example/config](https://github.com/viridIT/vSMTP/tree/main/examples/config) folder.

Backup the `vmstp.toml` file. Open with your favorite editor. Remove everything.
We will build it step-by-step.

```toml
version_requirement = ">=0.10.0, <1.0.0"  
// Version requirement. Do not remove or modify it 

[server]
domain = "doe-family.com"         

[server.interfaces]
addr = ["192.168.1.254:25"]
addr_submission = ["192.168.1.254:587"]
addr_submissions = ["192.168.1.254:465"]

[smtps]
security_level = "May"
protocol_version = ["TLSv1.3"]
fullchain = "/etc/vsmtp/certs/certificate.crt"
private_key = "/etc/vsmtp/certs/private.key"

[reply_codes]
Code220 = "220 Doe family ESMTP Service ready\r\n"
```

Quite simple, isn't it ? 

Next we have to define the rules to apply to a message. This is the role of vSL.

## vSL : the vSMTP Scripting Language

End users can easily define the behavior of vSMTP thanks to a simple but powerful programming language, the vSMTP Scripting Language (vSL).

vSL is based on three main concepts : objects, actions and rules.

Objects are virtual crates dedicated to manipulating mailboxes, ip addresses etc.
Actions basically used to accept, deny or quarantine a message.
Rules manipulate objects and actions at different stages of a SMTP transaction.

The `main.vsl` file is the entry point for vSL. By default it is located in the `/etc/vsmtp/rules` directory.

## Defining objects

Objects are declared through the "object" keyword. The basic syntax is:

```c
object <name> <type> = "<value>";
```

Many types are available. Let's define together all the required objects for Doe's MTA.
Open your favorite editor and create a file `objects.vsl` in the rule directory.

___/etc/vsmtp/rules/objects.vsl___

```c
// IP addresses of the MTA and the internal IP range
object local_mta ip4 "192.168.1.254";
object internal_net rg4 "192.168.0.0/24";

// Doe's family domain name
object local_fqdn fqdn "doe-family.com"

// The mailboxes
object john address "john.doe@doe-family.com";
object jane address "jane.doe@doe-family.com";
object jimmy address "jimmy.doe@doe-family.com";
object jenny address "jenny.doe@doe-family.com";

// A group to manipulate the mailboxes
object doe_family group [john, jane, jimmy, jenny];

// A quarantine for unknown mailboxes
object unknown_quarantine string "doe/bad_user";

// A user blacklist file
object user_blacklist file "user_blacklist.txt";
```

## Defining rules

___/etc/vsmtp/rules/main.vsl___

```c
// Import the object file
import "objects" as obj;

#{
  mail: [
    // Anti-relaying 
    rule "mail_norelay" || if (ctx.mail_from in my_obj::doe_family) && !(ctx.client_addr in my_obj::internal_net) 
      { vsl::deny() } else { vsl::accept() },
    // Paranoid
    rule "mail_default" || vsl::deny(), 
  ],
  rcpt: [
    // Outgoing mails
    rule "rcpt_outgoing" || if ctx.client_addr in my_obj::internal_net { vsl::accept() } else { vsl::next() },
    // Incoming mails - anti-relaying 
    rule "rcpt_norelay" || if ctx.rcpt.domains != my_obj::local_fqdn { vsl::deny() } else { vsl::next() },
    // Quarantine unknown users
    rule "rcpt_nouser" || if !(ctx.rcpt in my_obj::doe_family) { vsl::quarantine(user_quarantine) }, 
    // Jenny is 11 years old - emails are bcc to jane
    action "rcpt_jenny" || if ctx.rcpt is "jenny" { vsl::bcc(jane) },
    // Trailing rule 
    rule "rcpt_default" || vsl::accept(),
  ],
  deliver: [
    // Using IMAP in local Unix directory
    action "deliv_local" || vsl::deliver(ctx, maildir),
  ]
}
```
