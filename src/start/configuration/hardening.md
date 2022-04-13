# Hardening vSMTP








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
