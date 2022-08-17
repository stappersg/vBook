# Hardening vSMTP

## Disabling open relay

Doe's family server is connected to the Internet and must not be configured as an [open mail relay] that could be used by spammers and other malicious users.

[open mail relay]: https://en.wikipedia.org/wiki/Open_mail_relay

Here are the minimum set of rules for a properly configured server. It will only accept messages from the Internet:

- If the recipient is a Doe's family account, whatever the sender is.
- If the sender is authenticated as a Doe's family account, whatever the recipient is.

All IPs from the internal network are allowed to send messages.

Edit your `main.vsl` file and add the rules below.

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

> You can find more information about the SPF protocol in the [advanced section].

[advanced section]: ../../advanced/eam/spf.md

The SPF protocol allows other MTAs to check that outgoing messages from Doe's family domain are valid. A new DNS record is added into the `doe-family.com` DNS zone. It declares that only the server declared in the MX record is allowed to send messages on behalf of Doe's family.

```shell
doe-family.com.          TXT "v=spf1 +mx -all"
```

For incoming messages, the SPF protocol is configured to check the sender credentials at the `mail` stage. Edit your `main.vsl` code and just add the "check spf" rule.

```javascript
// -- main.vsl
#{
  mail: [
    rule "check spf" || check_spf("both", "soft"),
  ]
}
```

## Using DKIM

`Under construction`
