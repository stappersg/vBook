# Examples

## Personal MTA/MDA

### Context

A personal MTA for Doe's family.

Domain name : foo.bar
Users : john.doe@foo.bar, jane.doe@foo.bar, jimmy.doe@foo.bar, jenny.doe@foo.bar

### Network configuration

Doe's family has a router/firewall to route and secure their home network.
There's a small server in the DMZ to manage the family website, emails, etc.

vSMTP is installed on an Ubuntu server 20.04 virtual instance.

```console
{ Internet ISP } --- Firewall --- { DMZ : MTA }
                        |
              { Internal Network }
```

- Public IP : 80.80.80.80
- DMZ MTA IP : 192.168.1.254/32
- Internal Network : 192.168.0.0/24

___Firewall rules___

```shell
# Pseudo code - depends on your FW
#
# Allow SMTP and IMAP from Internet to MTA
Public IP > MTA : TCP/SMTP 25, TCP/SMTP 465, TCP/SMTP 587
# Allow viewing family emails using IMAP/ssl from the Internet 
Public IP > MTA : IMAP/ssl 993 
# Outgoing SMTP traffic
Internal NET > MTA : TCP/SMTP 25, TCP/SMTP 465, TCP/SMTP 587
MTA > {Internet} : TCP/SMTP 25, TCP/SMTP 465, TCP/SMTP 587
# DNS traffic from MTA
MTA > {Internet} : UDP/DNS 53, TCP/DNS 53
```

___DNS___

```shell
MX preference = 1, mail exchanger = vsmtp.foo.bar
```

### vSMTP configuration

___/etc/vsmtp/rules/object.vsl___

```c
obj ip4 "local_mta" "192.168.1.254";
obj rg4 "internal_net" "192.168.0.0/24";

obj fqdn "local_fqdn" "foo.bar"

obj addr "john" "john.doe@foo.bar";
obj addr "jane" "jane.doe@foo.bar";
obj addr "jimmy" "jimmy.doe@foo.bar";
obj addr "jenny" "jenny.doe@foo.bar";

obj grp "doe_family" [john, jane, jimmy, jenny];

obj str "user_quarantine" "doe/bad_user";

export local_mta, internal_net, local_fqdn, doe_family, john, jane, jimmy, jenny, user_quarantine;
//
// IMHO this is not the right way 
//
```

___/etc/vsmtp/rules/main.vsl___

```c
import "objects" as my_obj;

#{
  mail: [
    // Anti-relaying 
    rule "mail_norelay" || if (ctx.mail_from in my_obj::doe_family) && !(ctx.client_addr in my_obj::internal_net) 
      { vsl::deny() } else { vsl::accept() },
      //
      // We must reply sthing like : 554 5.7.1 <local_part@fqdn>: relay access denied
      //
    // Paranoid
    rule "mail_default" || vsl::deny(), 
  ],
  rcpt: [
    // Outgoing mails
    rule "rcpt_outgoing" || if ctx.client_addr in my_obj::internal_net { vsl::accept() } else { vsl::next() },
    // Incoming mails - anti-relaying 
    rule "rcpt_norelay" || if ctx.rcpt.domains != my_obj::local_fqdn { vsl::deny() } else { vsl::next() },
      //
      // We must reply sthing like : 554 5.7.1 <local_part@fqdn>: relay access denied
      //
    // Quarantine unknown users
    rule "rcpt_nouser" || if !(ctx.rcpt in my_obj::doe_family) { vsl::quarantine(user_quarantine) }, 
    // Jenny is 11 years old - emails are bcc to jane
    action "rcpt_jenny" || if ctx.rcpt is "jenny" { vsl::bcc(jane) },
    // Trailing rule 
    rule "rcpt_default" || vsl::accept(),
  ]
}
```

___vsmtp.toml___

```toml
[server]
domain = "foo.bar"
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
