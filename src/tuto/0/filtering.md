# Filtering

By default, the server will deny any SMTP transaction. We have to define [filtering rules](../../filtering/rules.md) to accept connections and filter messages.

In this chapter, you will get a glimpse of vSMTP's filtering system. To create your own filtering rules, we recommend checking out the [vSL reference](../../filtering/vsl.md), focussing on the following chapters:
* [Rules](../../filtering/rules.md)
* [SMTP Stages](../../filtering/stages.md)
* [Transaction context](../../filtering/transaction.md)

For this example, we will configure the following rules:

- Messages from blacklisted domain will be rejected.
- As Jenny is 11 years old, Jane wants her address to be added as a blind carbon copy of messages destined to her daughter.
- Messages sent to the family must be delivered in Mailbox format.

## Root incoming

In the [`Listen and serve`](##listen-and-serve) section of the previous chapter, we defined `/etc/vsmtp/domain-enabled` as the rule folder. Let's start with the root `incoming.vsl` script in this directory.

```diff
/etc/vsmtp/
 ┣ vsmtp.vsl
 ┣ conf.d/
 ┃      ┣ config.vsl
 ┃      ┗ *.vsl
+┣ domain-enabled/
+┃      ┗ incoming.vsl
 ┗ objects/
        ┗ family.vsl
```
<p class="ann"> <i>Adding the root filtering script</i> </p>

The `incoming.vsl` file is responsible for handling clients that just connected to vSMTP.

Let's setup anti-relaying by adding the following rule. (See the [Root Incoming](../../filtering/transaction.md##root-incoming) section in the [Transaction Context](../../filtering/transaction.md) chapter for more details)

```js
 #{
  rcpt: [
    rule "anti relaying" || deny(),
  ]
 }
```
<p class="ann"> <i>/etc/vsmtp/domain-enabled/incoming.vsl</i> </p>

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
<p class="ann"> <i>/etc/vsmtp/domain-enabled/incoming.vsl</i> </p>

The "do not deliver untrusted domains" rule will save any email from senders  addresses that match the `family::untrusted` regex in a quarantine folder named "untrusted", and will not deliver the email.

## Filtering for doe-family.com

Let's create filtering rules for the `doe-family.com` domain.

```diff
/etc/vsmtp
  ┣ vsmtp.vsl
  ┣ conf.d/
  ┃      ┣ config.vsl
  ┃      ┗ *.vsl
  ┣ domain-available/
+ ┃      ┗ doe-family.com/
+ ┃         ┣ incoming.vsl
+ ┃         ┣ outgoing.vsl
+ ┃         ┗ internal.vsl
  ┣ domain-enabled/
  ┃     ┣ incoming.vsl
+ ┃     ┗ example.com -> /etc/vsmtp/domain-available/doe-family.com
  ┗ objects/
       ┗ family.vsl
```
<p class="ann"> <i>adding filtering scripts for the doe-family.com domain</i> </p>

vSMTP will pickup `incoming.vsl`, `outgoing.vsl` and `internal.vsl` scripts under a folder with a fully qualified domain name. Those rules will be run following [vSMTP's transaction logic](../../filtering/transaction.md). Let's define rules for each cases.
