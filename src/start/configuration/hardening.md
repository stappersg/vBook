# Hardening vSMTP

## Disabling open relay

Doe's family server is connected to the Internet. It must not be configured to accept mail from any sender and deliver it to any recipient. This is an undesirable setup as it can be exploited by spammers and other malicious users.

Here are the strict minimum rules for a properly configured server. It will only accept messages from outside:

- If the recipient is a Doe's family account, whatever the sender.
- If the sender is authenticated as a Doe's family account, whatever the recipient.

All IPs from the internal network are allowed to send messages.

Edit your `main.vsl` code and just add the rule below.

```javascript
// -- main.vsl
import "objects" as obj;

#{
  rcpt: [
    rule "check relay" || check_relay(obj::internal_net),
  ],
}
```

## Using the SPF protocol

> You can find more information about SPF protocol in the [advanced section].

[advanced section]: ../../advanced/eam/spf.md

To allow other MTAs to verify that outgoing email from Doe's family domain comes from its server, we need to enable the SPF protocol. This is done by adding a new DNS text record that only allows only the MX record to send a mail for doe-family.com.

```shell
doe-family.com.          TXT "v=spf1 +mx -all"
```

That's all for outgoing messages. What about incoming messages ? Easier.

Edit your `main.vsl` code and just add the "check spf" rule.

```javascript
// -- main.vsl
#{
  mail: [
    rule "check spf" || check_spf("mail_from", "spf");
  ]
}
```

### Adding an antivirus

John is aware of security issues. Malware remains a scourge on the internet.
So he decides to add a second layer of antivirus.

Therefore, he installed [ClamAV](https://www.clamav.net/) which comes with the `clamsmtpd` daemon. We can use
smtp delegation to bridge the MTA and the antivirus.

```javascript
// -- service.vsl
service clamsmtpd smtp = #{
    delegator: #{
        address: "127.0.0.1:10026",
        timeout: "60s",
    },
    receiver: "127.0.0.1:10024",
};
```

```toml
# -- vsmtp.toml
version_requirement = ">=1.0.0"

[server.interfaces]
#      clients             delegation results
addr = ["127.0.0.1:10025", "127.0.0.1:10024"]
```

Since there is no heavy network traffic, John decided to do a pre-queue filtering.
Compromised emails are quarantined in the `virus_q` folder.

```js
// -- main.vsl
import "service" as s;

#{
    preq: [
        delegate s::clamsmtpd "check email for virus" || {
          // clamav inserts the "X-Virus-Infected" header
          // once a virus is detected. 
          if has_header("X-Virus-Infected") {
            quarantine("virus_q")
          } else {
            next()
          }
        }
    ],
}
```

Checkout the [Delegation section](delegation.md) to read more about the delegation mechanism.