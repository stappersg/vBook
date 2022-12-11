# Incoming messages

The `doe-family.com/incoming.vsl` script is run when the sender of the domain is not `doe-family.com` and that recipients domains are `doe-family.com`.

Thus, when this script is run, all recipients are guaranteed to have the `doe-family.com` domain. We can then deliver emails locally using the Mailbox protocol.

```js
import "objects/family" as family;

#{
  delivery: [
    action "setup delivery" || {
      for rcpt in rcpt_list() {
        // Deliver locally using Mailbox if the recipient is from Doe's family.
        if rcpt in family::family_addr { mailbox(rcpt) }
      }
    }
  ],
}
```

<p class="ann"> doe-family.com/incoming.vsl </p>

Jane wants a blind copy of her Jenny's messages. Let's create a Rhai function that does exactly that.

```diff
/etc/vsmtp
 ┣ vsmtp.vsl
 ┣ conf.d/
 ┃      ┣ config.vsl
 ┃      ┗ *.vsl
 ┣ domain-available/
 ┃      ┗ doe-family.com/
+┃         ┣ bcc.vsl
 ┃         ┣ incoming.vsl
 ┃         ┣ outgoing.vsl
 ┃         ┗ internal.vsl
 ┣ domain-enabled/
 ┃     ┣ incoming.vsl
 ┃     ┗ example.com -> ...
 ┗ objects/
       ┗ family.vsl
```

<p class="ann"> adding a new script to the domain </p>

```js
import "objects/family" as family;

fn bcc_jenny() {
  // add Jane as a blind carbon copy if the current recipient is Jenny.
  if rcpt() == family::jenny {
    bcc(family::jane)
  }
}
```

<p class="ann"> doe-family.com/bcc.vsl </p>

Now, let's plug this function to our filtering rules by importing the `bcc.vsl` script.

```diff js
+ import "domain-available/doe-family.com/bcc" as bcc;
  import "objects/family" as family;

  #{
+   rcpt: [
+     action "bcc jenny" || bcc::bcc_jenny(),
+   ],

    delivery: [
      action "setup delivery" || {
        for rcpt in rcpt_list() {
          // Deliver locally using Mailbox if the recipient is from Doe's family.
          if rcpt in family::family_addr { mailbox(rcpt) }
        }
      }
    ],
  }
```

<p class="ann"> doe-family.com/incoming.vsl </p>

With Rhai modules and functions, it becomes easy to reuse code across different rules.
