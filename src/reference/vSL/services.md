## Services

External services (third-party software) features come with releases 0.9.x.

### Shell services

Example : calling clamAV antivirus through clamscan command line.

___vsmtp.toml___

```toml
[rules]
dir = "

... //config 

[[rules.services]]
name = "antivirus"
type = "shell"
timeout = "15s"
command = "./service/clamscan.sh"
args = "{mail}"
```

___main.vsl___

```c
object str "virus_q" "my_quarantines/virus"

fn has_virus(services, ctx) {
    let result = services.run("antivirus", ctx);
    if result.has_signal {
        // timed out
        return false;
    }
    result.has_code && result.code != 0
}

run_rules!(
    #{
    preq: [
        action "antivirus" || {
            if has_virus(services, ctx) {
                vsl::quarantine(virus_q)
            }
        }
    ]
    }
)
```

___clamscan.sh___

```bash
#!/bin/bash
echo $1 | clamscan -
exit $?
```

### Unix socket services

// TO DO

### TCP/IP socket services

// TO DO
