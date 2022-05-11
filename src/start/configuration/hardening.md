# Hardening vSMTP

## Disabling open relay

Doe's family server is connected to the Internet. It must not be configured to accept mail from any sender and deliver it to any recipient. This is an undesirable setup as it can be exploited by spammers and other malicious users.

Here are the strict minimum rules for a properly configured server. It will only accept messages from outside:

- If the recipient is a Doe's family account, whatever the sender.
- If the sender is authenticated as a Doe's family account, whatever the recipient.

All IPs from the internal network are allowed to send messages.

Don't be afraid. vSMTP will do it for you.

Edit your main.vsl code and just add the rule below.

___main.vsl___
```javascript

fn check_relay(internal_net) {

    let srv_domain = in_domain();

    if !(ctx().is_authenticated || (ctx().client_ip in internal_net)) 
        && (ctx().rcpt.domain != srv_domain) {
            delete_rcpt(ctx().rcpt);
            info(code::code554_7_1)
    } else {
      sys::next()
    }
}

#{
  rcpt: [
    // the `check_relay` function will be available
    // in the standard vsl api in vsmtp 1.1
    rule "check relay" || check_relay(internal_net);
  ]
}
```

## Using the SPF protocol

> This is a v1.1 draft

To allow other MTAs to verify that outgoing email from Doe's family domain comes from its server, we need to enable the SPF protocol. This is done by adding a new DNS text record that only allows only the MX record to send a mail for doe-family.com.

You can find more information about SPF protocol in the [advanced section].

[advanced section]: ../../advanced/eam/spf.md

```shell
doe-family.com.          TXT "v=spf1 +mx -all"
```

That's all for outgoing messages. What about incoming messages ? Easier.

Edit your main.vsl code and just add the "check spf" rule.

___main.vsl___

```javascript
#{
  ...
  mail: [
    rule "check spf" || check_spf();
  ]
}
```

Couldn't be simpler, right ?

> To discover what is behind the `check_spf` function, go to the advanced section, [the vSL magic garden explained].

[the vSL magic garden explained]: ../../advanced/magic.md

### Adding an antivirus

John is aware of security issues. Malware remains a scourge on the internet.
So he decided to add a second layer of antivirus, directly on the vSMTP MTA.

He therefore installed ClamAV which comes with an online shell command, easily callable from vSMTP.

___services.vsl___

```javascript
services antivirus shell = #{
  timeout = "15s",
  command = "./service/clamscan.sh",
}
```

Since there is no heavy network traffic, John decided to do a pre-queue filtering.
Spool emails are quarantine in the virus_q folder.

___main.vsl___

```js

import "services" as s;
import "object" as obj;

fn has_virus(antivirus) {
    // we run clamscan with the email content.
    let result = antivirus.run_shell([ ctx().mail ]);
    // we check the result of clamscan.
    if result.has_signal {
        // timed out
        return false;
    }
    result.has_code && result.code != 0
}

#{
  preq: [
    rule "clam_av" || if has_virus(s::antivirus) { quarantine(obj::virus_queue) } else { accept() } 
  ]
}
```

___clamscan.sh___

```bash
#!/bin/bash
echo $1 | clamscan -
exit $?
```
