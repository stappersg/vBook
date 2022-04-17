# Basic configuration

Several examples can be found in the [example/config](https://github.com/viridIT/vSMTP/tree/main/examples/config) folder.

## The configuration file

`vsmtp.toml` is the main configuration file. It is located in `/etc/vsmtp` directory. Backup the `vmstp.toml` file. Open it with your favorite editor. Remove everything.
We will build it step-by-step.

```toml
# Version requirement. Do not remove or modify it 
version_requirement = ">=0.10.0, <1.0.0"  

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

Quite simple, isn't it ? 

Now that the server is configured we need to define the rules to apply to a message. This is the role of vSL.

## vSL : the vSMTP Scripting Language

End users can easily define the behavior of vSMTP thanks to a simple but powerful programming language, the vSMTP Scripting Language (vSL). vSL is based on three main concepts : `objects`, `actions` and `rules`.

`Objects` are virtual crates dedicated to manipulating mailboxes, ip addresses etc.
`Actions` are basically used to call a function.
`Rules` manipulate objects and actions at different stages of a SMTP transaction and then return a status code to the engine.

The `main.vsl` file is the entry point for vSL. By default it is located in the `/etc/vsmtp/rules` directory.

### RHAI and vSL

Commodo consequat aute ipsum excepteur sit exercitation cupidatat non elit non. Nisi dolor nostrud ex ut ex ullamco quis officia nulla aliqua. Sunt dolore ut mollit consectetur eiusmod dolor do enim aute duis magna aliqua ad.

### Defining objects

Objects are declared through the "object" keyword. The basic syntax is:

```c
object <name> <type> = "<value>";
```

Many types are available. Let's define together all the required objects for Doe's MTA.
Open your favorite editor and create a `objects.vsl` file in the rule directory.

___/etc/vsmtp/rules/objects.vsl___

```c
// IP addresses of the MTA and the internal IP range
object local_mta ip4 "192.168.1.254";
object internal_net rg4 "192.168.0.0/24";

// Doe's family domain name
object family_domain fqdn "doe-family.com"

// The mailboxes
object john address "john.doe@doe-family.com";
object jane address "jane.doe@doe-family.com";
object jimmy address "jimmy.doe@doe-family.com";
object jenny address "jenny.doe@doe-family.com";

// A group to manipulate the mailboxes
object family_addr group [john, jane, jimmy, jenny];

// A quarantine for unknown mailboxes
object unknown_quarantine string "doe/bad_user";

// A user blacklist file
object user_blacklist file "user_blacklist.txt";
```

Done. Easy right ? now we need to apply some rules on these objects. It's a bit more complicated but we're still working on making it more human readable.

## Defining rules and actions

Rules are the entry point to interact with the SMTP traffic at a user level. They are defined in the `/etc/vsmtp/rules/main.vsl` file.

Rules and action have the same syntax, except the first keyword.

```c
rule "name" || {              |       action "name" || {
    ... rule body.            |           ... action body.
}                             |       }
```

Let's add some rules in the main.vsl file for Doe's family MTA. There are two main constraints:

- Jenny is 11 years old, Jane wants a blind copy of her daughter messages.
- They use IMAP and Maildir format

___/etc/vsmtp/rules/main.vsl___

```c
// Import the object file. The 'doe' prefix permits to distinguish Doe's family objects from others.
import "objects" as doe;

#{

  // Actions and rules triggered in the RCPT TO: stage.

  mail: [
   rule "anti-relay" || if (ctx.mail_domain in my_domain) && ((ctx.client_ip in local_network) || (ctx.client.auth))
          { vsl::accept() }
        else
          { vsl::deny() }
  ],

  rcpt: [
    action "rcpt_jenny" || if doe::jenny in ctx.rcpt { vsl::bcc(doe::jane) },
  ],


  deliver: [
    // Using IMAP in local Unix directory

    action "delivery" || 
      for rcpt in ctx.rcpt {
        if rcpt in family_addr { vsl::maildir(ctx, rcpt) } else { vsl::deliver(ctx, rcpt) }
      }
  ]
}



```
