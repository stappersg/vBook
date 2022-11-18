# Filtering

By default, the server will deny any SMTP transaction. We have to define [filtering rules](/src/reference/vSL/rules.md) to accept connections and filter messages.

In this chapter, you will get a glimpse of vSMTP's filtering system. To create your own filtering rules, we recommend checking out the [vSL reference](/src/reference/vSL/vsl.md), focussing on the following chapters:
* [Rules](/src/reference/vSL/rules.md)
* [SMTP Stages](/src/reference/vSL/stages.md)
* [Transaction context](/src/reference/vSL/transaction.md)

For this example, will configure the following rules:

- Messages from blacklisted domain will be rejected.
- As Jenny is 11 years old, Jane wants her address to be added as a blind carbon copy of messages destined to her daughter.
- Messages sent to the family must be delivered in Mailbox format.

## Root incoming

In the [`Listen and serve`](##listen-and-serve) section of the previous chapter, we defined `/etc/vsmtp/domain-available` as the rule folder. Let's start with the root `incoming.vsl` script in this directory.

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

Let's setup anti-relaying by adding the following rule. (See the [Root Incoming](/src/reference/vSL/transaction.md##root-incoming) section in the [Transaction Context](/src/reference/vSL/transaction.md) chapter for more details)

```js
 #{
  rcpt: [
    rule "anti relaying" || deny(),
  ]
 }
```
<p style="text-align: center;"> <i>/etc/vsmtp/domain-available/incoming.vsl</i> </p>

We can add a blacklist of sender domains that we do not trust too.

```diff js
// Importing objects that we defined in the last chapter.
+import "objects/family" as family;

#{
+ mail: [
+   rule "do not deliver untrusted domains" || {
+       if mail_from() in family::untrusted {
+           quarantine("untrusted")
+       } else {
+           next()
+       }
+   },
+ ],

  rcpt: [
    rule "anti relaying" || deny(),
  ]
}
```
<p style="text-align: center;"> <i>/etc/vsmtp/domain-available/incoming.vsl</i> </p>

the "do not deliver untrusted domains" rule will save any email from senders  addresses that match the `family::untrusted` regex in a quarantine folder named "untrusted", and will not deliver the email.

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

vSMTP will pickup `incoming.vsl`, `outgoing.vsl` and `internal.vsl` scripts under a folder with a fully qualified domain name. Those rules will be run following [vSMTP's transaction logic](/src/reference/vSL/transaction.md). Let's define rules for each cases.

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

Jane wants a blind copy of her Jenny's messages. Let's create a Rhai function that does exactly that.

```diff
/etc/vsmtp
 ┣ vsmtp.vsl
 ┣ conf.d/
 ┃      ┣ config.vsl
 ┃      ┗ *.vsl
 ┣ domain-available/
 ┃      ┣ incoming.vsl
 ┃      ┗ doe-family.com/
+┃         ┣ bcc.vsl
 ┃         ┣ incoming.vsl
 ┃         ┣ outgoing.vsl
 ┃         ┗ internal.vsl
 ┗ objects/
       ┗ family.vsl
```
<p style="text-align: center;"> <i>adding a new script to the subdomain</i> </p>

```js
import "objects/family" as family;

fn bcc_jenny() {
    // add Jane as a blind carbon copy if the current recipient is Jenny.
    if rcpt() == family::jenny {
      bcc(family::jane)
    }
}
```
<p style="text-align: center;"> <i>doe-family.com/bcc.vsl</i> </p>

Now, let's plug this function to our filtering rules by importing the `bcc.vsl` script.

```diff js
+ import "domain-available/doe-family.com/bcc" as bcc;
  import "objects/family" as family;

  #{
+   rcpt: [
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
<p style="text-align: center;"> <i>doe-family.com/incoming.vsl</i> </p>

With Rhai modules and functions, it becomes easy to reuse code across different rules.

### doe-family.com outgoing messages

`doe-family.com/outgoing.vsl` is run when the sender of the domain is `doe-family.com` and that recipients domains are not `doe-family.com`.

Here, a member of Doe's family is sending an email to someone else. We just have to verify that the sender is legitimate by asking the client to authenticate itself to vSMTP. If the authentication fails, this probably means that a spammer tried to use our server as a relay. The `authenticate()` function automatically denies the transaction if the authentication failed.

```js
#{
  mail: [
    rule "authenticate" || authenticate(),
  ]
}
```
<p style="text-align: center;"> <i>doe-family.com/outgoing.vsl</i> </p>

> ⚠️ The `authenticate()` function uses the `testsaslauthd` program under the hood, itself calling the `saslauthd` daemon.
> Make sure to install the [Cyrus sasl binary package](https://www.cyrusimap.org/sasl/)for your distribution and configure the `saslauthd` daemon with `MECHANISM="shadow"` in `/etc/default/saslauthd`.

### doe-family.com internal messages

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

## Conclusion

After setting up all filtering scripts above, our vSMTP instance is able to:

- Block messages from blacklisted domain.
- Add Jane's address as a blind carbon copy when Jenny receives a message.
- Deliver messages locally to all members of the family.

Simply restart the server to apply the rules.

```sh
$> sudo systemd restart vsmtp
$> telnet 192.168.1.254:25
220 doe-family.com Service ready
554 permanent problems with the remote server
```