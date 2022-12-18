# Filtering

By default, the server will deny any SMTP transaction. We have to define [filtering rules](../../filtering/rules.md) to accept connections and filter messages.

In this chapter, we will get a glimpse of vSMTP's filtering system. To create filtering rules, we recommend checking out the [vSL reference](../../filtering/vsl.md), focussing on the following chapters:
* [Rules](../../filtering/rules.md)
* [SMTP Stages](../../filtering/stages.md)
* [Transaction context](../../filtering/transaction.md)

For this example, we will configure the following rules:

- Messages from blacklisted domain will be rejected.
- As Jenny is 11 years old, Jane wants her address to be added as a blind carbon copy of messages destined to her daughter.
- Messages sent to the family must be delivered in Mailbox format.

## Configuration

Let's first add our filters in the `/etc/vsmtp/conf.d/config.vsl` script.

```diff,rust,ignore
  fn on_config(config) {
    // Name of the server.
    config.server.name = "doe-family.com";

    // addresses that the server will listen to.
    // (change `192.168.1.254` for the desired address)
    config.server.interfaces = #{
      addr: ["192.168.1.254:25"],
      addr_submission: ["192.168.1.254:587"],
      addr_submissions: ["192.168.1.254:465"],
    };

+  // Root filter.
+  config.app.vsl.filter_path = "/etc/vsmtp/filter.vsl";
+  // Domain specific filters.
+  config.app.vsl.domain_dir = "/etc/vsmtp/domain-enabled";

    config
  }
```

## Root Filter

Let's define the root filter for incoming emails.

```diff
/etc/vsmtp/
 ┣ vsmtp.vsl
+┣ filter.vsl
 ┣ conf.d/
 ┃      ┣ config.vsl
 ┃      ┗ *.vsl
 ┗ objects/
        ┗ family.vsl
```
<p class="ann"> Adding the root filtering script </p>

The `filter.vsl` script is responsible for handling clients that just connected to vSMTP.

### Add anti-relaying

Let's setup anti-relaying by adding the following rule. (See the [Root Filter](../../filtering/transaction.md#root-filter-⬜) section in the [Transaction Context](../../filtering/transaction.md) chapter for more details)

```
#{
  rcpt: [
    rule "anti relaying" || deny(),
  ]
}
```
<p class="ann"> /etc/vsmtp/filter.vsl </p>

### Use the blacklist

We can add the blacklist we defined in the [Blacklist section](basic.md#blacklist) to filter out sender domains that we do not trust.

```diff,rust,ignore
// Importing objects that we defined in the last chapter.
+import "objects/family" as family;

#{
+ mail: [
+   rule "do not deliver untrusted domains" || {
+       if mail_from().domain in family::blacklist {
+           quarantine(family::untrusted_queue)
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
<p class="ann"> /etc/vsmtp/filter.vsl </p>

The `do not deliver untrusted domains` rule will save any email from senders found in the blacklist in a quarantine folder named "untrusted" and will not deliver the email.

## Filtering for doe-family.com

Let's create filtering rules for the `doe-family.com` domain.

```diff
/etc/vsmtp
  ┣ vsmtp.vsl
  ┣ filter.vsl
  ┣ conf.d/
  ┃      ┣ config.vsl
  ┃      ┗ *.vsl
+ ┣ domain-available/
+ ┃      ┗ doe-family.com/
+ ┃         ┣ incoming.vsl
+ ┃         ┣ outgoing.vsl
+ ┃         ┗ internal.vsl
+ ┣ domain-enabled/
  ┗ objects/
       ┗ family.vsl
```
<p class="ann"> adding filtering scripts for the `doe-family.com` domain </p>

Since we specified in the configuration that the `domain-enabled` directory was our domain filtering directory, we need to create a symbolic link to `domain-available/doe-family.com` to enable filtering for `doe-family.com`.

```diff
/etc/vsmtp
  ┣ vsmtp.vsl
  ┣ filter.vsl
  ┣ conf.d/
  ┃      ┣ config.vsl
  ┃      ┗ *.vsl
  ┣ domain-available/
  ┃      ┗ doe-family.com/
  ┃         ┣ incoming.vsl
  ┃         ┣ outgoing.vsl
  ┃         ┗ internal.vsl
  ┣ domain-enabled/
+ ┃     ┗ example.com -> /etc/vsmtp/domain-available/doe-family.com
  ┗ objects/
       ┗ family.vsl
```
<p class="ann"> Enabling the `example.com` domain filtering </p>

vSMTP will pickup `incoming.vsl`, `outgoing.vsl` and `internal.vsl` scripts under a folder with a fully qualified domain name. Those rules will be run following [vSMTP's transaction logic](../../filtering/transaction.md). Let's define rules for each cases.
