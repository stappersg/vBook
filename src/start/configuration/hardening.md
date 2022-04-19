# Hardening vSMTP

## Disabling open relay

Doe's family server is connected to the Internet. It must not be configured to accept mail from any sender and deliver it to any recipient. This is an undesirable setup as it can be exploited by spammers and other malicious users.

Here are the strict minimum rules for a properly configured server. It will only accept messages from outside:

- If the recipient is a Doe's family account, whatever the sender.
- If the sender is authenticated as a Doe's family account, whatever the recipient.

All IPs from the internal network are allowed to send messages.

Don't be afraid. vSMTP will do it for you.

Edit your main.vsl code and just add the the rule below.

```javascript
// main.vsl
import "/addons-std/api" as api;

rcpt: [
  rule "check relay" || vsl::check_relay(ctx, srv);
]
```

## Using the SPF protocol

> This is a v0.11 draft

To allow other MTAs to verify that outgoing email from Doe's family domain comes from its server, we need to enable the SPF protocol. This is done by adding a new DNS text record that only allows only the MX record to send a mail for doe-family.com.

You can find more information about SPF protocol in the [advanced section].

[advanced section]: advanced/eam/spf.md

```shell
doe-family.com.          TXT "v=spf1 +mx -all"
```

That's all for outgoing messages. What about incoming messages ? Easier.

Edit your main.vsl code and just add the "check spf" rule.

```javascript
// main.vsl
import "/addons-std/api" as api;

mail: [
  rule "check spf" || api::check_spf(ctx, srv);
]
```

Couldn't be simpler, right ?

> To discover what is behind the api::check_spf function, go to the advanced section, [the vSL magic garden explained].

[the vSL magic garden explained]: advanced/magic.md

### Adding an antivirus

John is aware of security issues. Malware remains a scourge on the internet.
So he decided to add a second layer of antivirus, directly on the vSMTP MTA.

He therefore installed ClamAV which comes with an online shell command, easily callable from vSMTP.

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
