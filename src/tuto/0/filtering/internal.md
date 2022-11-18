
# Internal messages

`doe-family.com/internal.vsl` is run when the sender and recipients domains are both  `doe-family.com`.

Since we already authenticated clients in `outgoing.vsl`, we simply have to setup delivery.

```js
// let's reuse our bcc code to add Jane as a blind carbon copy.
import "domain-available/doe-family.com/bcc" as bcc;

#{
  rcpt: [
      action "bcc jenny" || bcc::bcc_jenny(),
  ],

  delivery: [
      // Deliver all recipients locally.
      action "setup delivery" || mailbox_all(),
  ],
}
```
<p style="text-align: center;"> <i>doe-family.com/internal.vsl</i> </p>


Now that all filtering rules are set for the `doe-family.com` domain, let's restart the server to apply all rules.

```sh
$ sudo systemd restart vsmtp
$ telnet 192.168.1.254:25
```