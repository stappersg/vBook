# Filtering

By default, the server will deny any SMTP transaction. We have to define [filtering rules](/src/reference/vSL/rules.md) to accept connections and filter messages.

In this chapter, you will get a glimpse of vSMTP's filtering system. To create your own filtering rules, we recommend checking out the [vSL reference](/src/reference/vSL/vsl.md), focussing on the following chapters:
* [Rules](/src/reference/vSL/rules.md)
* [SMTP Stages](/src/reference/vSL/stages.md)
* [Transaction context](/src/reference/vSL/transaction.md)

For this example, will configure the following rules:

- Messages from blacklisted domain will be rejected.
- As Jenny is 11 years old, Jane wants a blind copy of her daughter messages.
- Messages sent to the family must be delivered in MailBox format.

## Root incoming

In the [`Listen and serve`](##listen-and-serve) section, we defined `/etc/vsmtp/domain-available` as the rule folder. Thus, let's start with the root `incoming.vsl` script in the `/etc/vsmtp/domain-available` directory.

```diff
/etc/vsmtp/
 ┣ vsmtp.vsl
 ┣ conf.d/
 ┃      ┣ config.vsl
 ┃      ┗ *.vsl
+┣ domain-available/
+┃      ┗ incoming.vsl
 ┗ objects/
        ┗ family.vsl
```
<p style="text-align: center;"> <i>Adding the root filtering script</i> </p>

The `incoming.vsl` file is responsible for handling clients that just connected to vSMTP.

Add the following rule to force client to authenticate.

```js
#{
  authenticate: [
    rule "auth" || authenticate(),
  ]
}
```
<p style="text-align: center;"> <i>/etc/vsmtp/domain-available/incoming.vsl</i> </p>

Now, setup anti-relaying by adding the following rule. (See the [Root Incoming](/src/reference/vSL/transaction.md##root-incoming) section in the [Transaction Context](/src/reference/vSL/transaction.md) chapter for more details)

```diff js
 #{
   authenticate: [
     rule "auth" || authenticate(),
   ],
+ 
+  rcpt: [
+    rule "anti relaying" || deny(),
+  ]
 }
```
<p style="text-align: center;"> <i>/etc/vsmtp/domain-available/incoming.vsl</i> </p>

## Filtering for doe-family.com

Let's create filtering rules for the `doe-family.com` domain.

```diff
/etc/vsmtp
 ┣ vsmtp.vsl
 ┣ conf.d/
 ┃      ┣ config.vsl
 ┃      ┗ *.vsl
 ┣ domain-available/
 ┃      ┣ incoming.vsl
+┃      ┗ doe-family.com/
+┃         ┣ incoming.vsl
+┃         ┣ outgoing.vsl
+┃         ┗ internal.vsl
┗ objects/
       ┗ family.vsl
```
<p style="text-align: center;"> <i>adding filtering scripts for the doe-family.com domain</i> </p>

vSMTP will pickup any `incoming.vsl`, `outgoing.vsl` and `internal.vsl` scripts under a folder with a fully qualified domain name. Those rules will be run following [vSMTP's transaction logic](/src/reference/vSL/transaction.md). Let's define rules for each case.

### doe-family.com incoming messages

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
<p style="text-align: center;"> <i>doe-family.com/incoming.vsl</i> </p>

Jane wants a blind copy of her Jenny's messages. Lets create

```js
import "objects/family" as obj;

fn bcc_jenny() {
    if rcpt() == obj::jenny { bcc(obj::jane) }
}
```

Now, let's add that plug this function to our filtering rules.

```diff js
+ import "domain-available/doe-family.com/bcc" as bcc;
  import "objects/family" as family;

  #{
+   rcpt: [
+       // Jane will always be added as a bcc when jenny is part of the recipients.
+       action "bcc jenny" || bcc::bcc_jenny(),
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


### doe-family.com outgoing messages

- `doe-family.com/outgoing.vsl` is run when the sender of the domain is `doe-family.com` and that recipients domains are not `doe-family.com`.

### doe-family.com internal messages

- `doe-family.com/internal.vsl` is run when the sender and recipients domains are both  `doe-family.com`.

# TODO: remove

```js
// -- /etc/vsmtp/rules/main.vsl
// Import the object file. The 'doe' prefix is an alias.
import "objects" as doe;

#{
  // List of rules execute after receiving "MAIL FROM" from a client.
  // At this stage the sender is known and can be accessed using `mail_from()`.
  mail: [
    // Deny any sender with a domain listed in the `blacklist` group.
    rule "blacklist" || {
      if mail_from().domain in doe::blacklist { deny() } else { next() }
    }
  ],

  // List of rules execute after receiving "RCPT TO" from a client.
  // The current recipient can be inspected using `rcpt()`.
  rcpt: [
    // automatically set Jane as a BCC if Jenny is part of the recipients.
    action "bcc jenny" || if rcpt() is doe::jenny { bcc(doe::jane) },
  ],

  // The delivery stage is executed just before vsmtp delivers the message.
  delivery: [
    action "setup delivery" || {
      // if a recipient is part of the family, we deliver the email locally.
      // Otherwise, we just deliver the email to another server.
      for rcpt in rcpt_list() {
        if rcpt in doe::family_addr { maildir(rcpt) } else { deliver(rcpt) }
      }
    }
  ]
}
```

Add these lines to your `/etc/vsmtp/vsmtp.vsl`:

Restart the server to apply the rules.
