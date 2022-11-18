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
