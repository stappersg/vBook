# Basic configuration

## vSMTP Configuration

Let's build a vSMTP configuration step by step.

When installing vSMTP, the package manager creates the following basic configuration.

```diff
/etc/vsmtp
+┣ vsmtp.vsl
+┗ conf.d/
+      ┗ config.vsl
```
<p class="ann"> vSMTP default configuration </p>

## Configure vSMTP

Modify the [`/etc/vsmtp/conf.d/config.vsl`](../../get-started/config-file-struct/root.md) file with this configuration:

```rust,ignore
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

  config
}
```
<p class="ann"> Configuring vSMTP </p>

> For complex configurations, it is recommended to split the file into [Rhai modules](https://rhai.rs/book/language/modules/index.html).

> To get an exhaustive list of parameters that can be changed in the configuration, see the [Configuration Reference](../../ref/vSL/api/var::cfg.md) chapter.

The server can now listen and serve SMTP connections.

## Filtering objects

Let's define all the required objects for John Doe's MTA. Those objects are used to configure vSMTP and simplify filtering rules.

Create the `/etc/vsmtp/objects/family.vsl` file with following objects:

```rust,ignore
// Doe's family domain name.
export const domain = fqdn("doe-family.com");

// Mailboxes.
export const john = address("john.doe@doe-family.com");
export const jane = address("jane.doe@doe-family.com");
export const jimmy = address("jimmy.doe@doe-family.com");
export const jenny = address("jenny.doe@doe-family.com");

export const addresses = [john, jane, jimmy, jenny];

// Paths for quarantines.
export const virus_queue = "virus";
export const untrusted_queue = "untrusted";

// A user blacklist file
export const blacklist = file("domain-available/example.com/blacklist.txt", "fqdn");
```
<p class="ann"> Objects that will be used during filtering </p>

> See the [Object chapter](../../filtering/objects.md) for more information.

## Blacklist

Define a blacklist file at `/etc/vsmtp/domain-available/example.com/blacklist.txt` with the following contents:

```text
domain-spam.com
spam-domain.org
domain-spammers.com
foobar-spam-pro.org
```
<p class="ann"> Blacklist content </p>

## Listen and serve

The file structure of `/etc/vsmtp` should now look like this.

```diff
/etc/vsmtp/
 ┣ vsmtp.vsl
 ┣ conf.d/
 ┃      ┗ config.vsl
 ┣ domain-available/
+┃      ┗ example.com/
+┃          ┗ blacklist.txt
+┗ objects/
+       ┗ family.vsl
```
<p class="ann"> Adding objects and the blacklist to the configuration directory </p>

> If no interface is specified, the server listens on localhost on port 25, 465 and 587. Remote connections are therefore refused.

```sh
$> sudo systemd restart vsmtp
$> telnet 192.168.1.254:25
# 220 doe-family.com Service ready
# 554 permanent problems with the remote server
```
<p class="ann"> Test by opening a connexion to the server </p>
