# Hardening vSMTP

## Adding an anti-relaying rule

TO DO

## Using the SPF protocol

> This is a v0.11 draft

To allow other MTAs to verify that outgoing email from Doe's family domain comes from its server, we need to enable the SPF protocol. This is done by adding a new DNS text record that only allows only the MX record to send a mail for doe-family.com.

You can find more information about SPF protocol in the [advanced section].

[advanced section]: (advanced/eam/spf.md).

```shell
doe-family.com.          TXT "v=spf1 +mx -all"
```

That's all for outgoing messages. What about incoming messages ? Easier.

Edit your main.vsl code and just add the "check_spf" rule.

```javascript
/// main.vsl
import "/addons-std/api" as api;

mail: [
  rule "check_spf" || api::check_spf(ctx);
]
```

Couldn't be simpler, right ?

> To discover what is behind the api::check_spf function, go to the advanced section, [the vSL magic garden explained].

[the vSL magic garden explained]: (advanced/magic.md)

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
