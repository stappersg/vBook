# Disabling [open mail relay](https://en.wikipedia.org/wiki/Open_mail_relay)

The server must only accept messages from the Internet that comply with :

- The recipient is an account from Doe's family, whatever the sender is (incoming messages).
- The sender is authenticated as an account from Doe's family, whatever the recipient is (outgoing messages).

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
