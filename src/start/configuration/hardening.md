# Hardening vSMTP

## Disabling open relay

Doe's family server is connected to the Internet. It must not be configured to accept mail from any sender and deliver it to any recipient. This is an undesirable setup as it can be exploited by spammers and other malicious users.

Here are the strict minimum rules for a properly configured server. It will only accept messages from outside:

- If the recipient is a Doe's family account, whatever the sender.
- If the sender is authenticated as a Doe's family account, whatever the recipient.

All IPs from the internal network are allowed to send messages.

Edit your `main.vsl` code and add the rules below.

```javascript
// -- main.vsl
import "objects" as doe;

#{
  mail: [
    rule "relay mail from" || check_mail_relay(doe::internal_net),
  ],

  rcpt: [
    rule "relay rcpt" || check_rcpt_relay(doe::internal_net),
  ],
}
```

Doe's family users must be authenticated if they send messages from an external network (i.e. from a cellular net). As John decided to create Unix users, the shadow mechanism is required.

```javascript
  authenticate: [
    rule "auth /etc/shadow" || {
        authenticate()
      }
    ],
```

> This is a temporary vSL code required by v1.1. Future releases will bring an out-of-the box vSL function. Do not forget to start saslauthd daemon with MECHANISM="shadow" in /etc/default/saslauthd.

Now Doe's family server is protected against open-relaying attacks.

## Using the SPF protocol

> You can find more information about SPF protocol in the [advanced section].

[advanced section]: ../../advanced/eam/spf.md

To allow other MTAs to verify that outgoing email from Doe's family domain comes from its server, we need to enable the SPF protocol. This is done by adding a new DNS text record that only allows only the MX record to send a mail for doe-family.com.

```shell
doe-family.com.          TXT "v=spf1 +mx -all"
```

That's all for outgoing messages. What about incoming messages ?

Edit your `main.vsl` code and just add the "check spf" rule.

```javascript
// -- main.vsl
#{
  mail: [
    rule "check spf" || check_spf("both", "soft"),
  ]
}
```
