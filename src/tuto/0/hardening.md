# Hardening vSMTP

## Disabling open relay

Doe's family server is connected to the Internet and must not be configured as an [open mail relay] that could be used by spammers and other malicious users.

[open mail relay]: https://en.wikipedia.org/wiki/Open_mail_relay

From the Internet, the server will only accept messages where:

- The recipient is a Doe's family account, whatever the sender is (incoming messages).
- The sender is authenticated as a Doe's family account, whatever the recipient is (outgoing messages).

From the internal network, all IPs are allowed to send messages.

Edit your `/etc/vsmtp/rules/main.vsl` file and add the rules:

```js
// -- main.vsl
import "objects" as doe;

#{
  // ... previous code ...

  mail: [
    rule "relay mail from" || check_mail_relay(doe::internal_net),
  ],

  rcpt: [
    rule "relay rcpt" || check_rcpt_relay(doe::internal_net),
  ],
}
```

Now Doe's family server is protected against open-relaying attacks.

## Using the [SPF](/advanced/eam/spf.md) protocol

The SPF protocol allows other MTAs to check that outgoing messages from Doe's family domain are valid. A new DNS record is added into the `doe-family.com` DNS zone. It declares that only the server declared in the MX record is allowed to send messages on behalf of Doe's family.

```shell
doe-family.com.          TXT "v=spf1 +mx -all"
```

For incoming messages, the SPF protocol is configured to check the sender credentials at the `mail` stage.

Edit your `/etc/vsmtp/rules/main.vsl` file and add the rule:

```js
// -- main.vsl
#{
  // ... previous code ...

  mail: [
    rule "check spf" || check_spf("both", "soft"),
  ]
}
```

## Using [DKIM](/advanced/eam/dkim.html)

`Under construction 🚧`
