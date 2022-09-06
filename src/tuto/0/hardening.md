# Hardening vSMTP

## Disabling [open mail relay](https://en.wikipedia.org/wiki/Open_mail_relay)

From the Internet, the server must accept only messages in accordance with :

- If the recipient is a Doe's family account, whatever the sender is (incoming messages).
- If the sender is authenticated as a Doe's family account, whatever the recipient is (outgoing messages).

From the internal network, all IPs are allowed to send messages.

Edit the `/etc/vsmtp/rules/main.vsl` file and add the rules:

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

Edit the `/etc/vsmtp/rules/main.vsl` file and add the rule:

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

The DKIM protocol is natively implemented in vSMTP.

This protocol ensure that the content of the message has not been modified during the transport. A new DNS record is added into the `doe-family.com` DNS zone. It declares the public key usable to verify the messages (see [how to had the DKIM record](/advanced/eam/dkim.html#dns-records)).

We will configure these rule:

- The sender is a Doe's family account : a DKIM signature is added to the message.
- The recipient is a Doe's family account : the DKIM signatures are verified.

Add the following to the `/etc/vsmtp/vsmtp.toml` file:

```toml
[server.dkim]
private_key = "/path/to/private-key"
```

Edit the `/etc/vsmtp/rules/main.vsl` file and add the rules:

```js
#{
  // ... previous code ...

  postq: [
    action "sign dkim" || {
      if in_domain(mail_from()) {
        dkim_sign("2022-09" /* selector of the DNS record */);
      } else {
        dkim_verify();
      }
    }
  ],
}
```
