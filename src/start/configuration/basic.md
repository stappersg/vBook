# Basic configuration

## The configuration file

Nulla amet cupidatat exercitation sit adipisicing deserunt culpa ex elit. Deserunt labore mollit labore commodo. Ex sunt excepteur amet eiusmod proident amet veniam reprehenderit eu ut sunt nisi elit elit. Excepteur eu minim minim non.



Examples can be found in repo....



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

___vsmtp.toml___

```toml
[server]
domain = "doe-family.com"
addr = "192.168.1.254:25"
addr_submission = "192.168.1.254:587"
addr_submissions = "192.168.1.254:465"

[logs]
file = "/var/log/vsmtp/vsmtp.log"

[logs.level]
default = "warn"

[rules]
dir = "/etc/vsmtp/rules"

[smtps]
security_level = "May"
capath = "/etc/vsmtp/certs"
preempt_cipherlist = true
handshake_timeout = "100ms"
protocol_version = ["TLSv1.3"]

fullchain = "{capath}/certificate.crt"
private_key = "{capath}/private.key"

[smtp]
rcpt_count_max = 25
disable_ehlo = false

[smtp.error]
soft_count = 5
hard_count = 10
delay = "5000ms"

[reply_codes]
Code214 = "214 my custom help message\r\n"
Code220 = "220 {domain} ESMTP Service ready\r\n"

[delivery]
spool_dir = "/var/spool/vsmtp"

[delivery.queues]
working = { capacity = 32 }
deliver = { capacity = 32 }
deferred = { retry_max = 10, cron_period = "10s" }
```

### Adding an antivirus

John is aware of security issues. Malware remains a scourge on the internet.
So he decided to add a second layer of antivirus, directly on the vSMTP MTA.

He therefore installs ClamAV which comes with an online shell command, easily callable from vSMTP.

___vsmtp.toml___

```toml
... //config 

[rules]
dir = "/etc/vsmtp/rules"

[[rules.services]]
name = "antivirus"
type = "shell"
timeout = "15s"
command = "./service/clamscan.sh"
args = "{mail}"

//
// quarantine_folder is missing
//

... //config 
```

Since there is no heavy network traffic, John decided to do a pre-queue filtering.
Spool emails are quarantine in the virus_q folder.

___main.vsl___

```c
fn has_virus(services, ctx) {
    let result = services.run("antivirus", ctx);
    if result.has_signal {
        // timed out
        return false;
    }
    result.has_code && result.code != 0
}

#{
  preq: [
    rule "clam_av" || if has_virus(services, ctx) { vsl::quarantine(virus_q) } else { vsl::accept() } 
  ]
}
```

___clamscan.sh___

```bash
#!/bin/bash
echo $1 | clamscan -
exit $?
```
