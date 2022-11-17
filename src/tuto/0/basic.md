# Basic configuration

## vSMTP Configuration

Let's build a vSMTP configuration step by step. For a full description of the configuration file hierarchy, read the [Configuring vSMTP](./../../get-started/config-file-struct.md) chapter.

When installing vSMTP, the package manager should create the following basic configuration.

```diff
/etc/vsmtp
+┣ vsmtp.vsl
+┗ conf.d/
+      ┗ config.vsl
```

> For more details on root configuration files, check out the [`Configuring vSMTP`](/src/get-started/config-file-struct.md###root-configuration) chapter.

## Listen and serve

First of all, modify the [`/etc/vsmtp/conf.d/config.vsl`](/src/get-started/config-file-struct.md###root-configuration) file with this configuration:

```js
fn on_config(config) {
  // Name of the server.
  config.server.name = "doe-family.com";

  // addresses that the server will listen to.
  // (change `192.168.1.254` for the address you want to listen to)
  config.server.interfaces = #{
    addr: ["192.168.1.254:25"],
    addr_submission: ["192.168.1.254:587"],
    addr_submissions: ["192.168.1.254:465"],
  };

  // The folder containing filtering rules.
  config.app.vsl.dirpath = "/etc/vsmtp/domain-available";

  config
}
```

> It is recommended to split the configuration into [Rhai modules](https://rhai.rs/book/language/modules/index.html).

> To get an exhaustive list of parameters that you can change in the configuration, see the [Configuration Reference](TODO:) chapter.

The server can now listen and serve SMTP connections.

Now, let's define all the required objects for John Doe's MTA. Those objects are used to configure vSMTP and simplify filtering rules.

Create the `/etc/vsmtp/objects/family.vsl` file with following objects:

```js
// IP addresses of the MTA and the internal IP range.
export const local_mta = ip4("192.168.1.254");
export const internal_net = rg4("192.168.0.0/24");

// Doe's family domain name.
export const domain = fqdn("doe-family.com");

// Mailboxes.
export const john = address("john.doe@doe-family.com");
export const jane = address("jane.doe@doe-family.com");
export const jimmy = address("jimmy.doe@doe-family.com");
export const jenny = address("jenny.doe@doe-family.com");

export const addresses = [john, jane, jimmy, jenny];

// Paths for quarantines.
export const unknown_quarantine = "doe/bad_user";
export const virus_queue = "doe/virus";

// A user blacklist file
export const blacklist = file("conf.d/blacklist.txt", "fqdn");
```

> See the [Object Reference](/src/reference/vSL/objects.md#Objects) chapter for more information.

Define a blacklist file at `/etc/vsmtp/conf.d/blacklist.txt` with the following contents:

```text
domain-spam.com
spam-domain.org
domain-spammers.com
foobar-spam-pro.org
```

The file structure of `/etc/vsmtp` should now look like this.

```diff
/etc/vsmtp/
 ┣ vsmtp.vsl
 ┣ conf.d/
 ┃      ┣ config.vsl
+┃      ┗ blacklist.txt
+┗ objects/
+       ┗ family.vsl
```

> If no interface is specified, the server listens on localhost on port 25, 465 and 587. Remote connections are therefore refused.

Now, restart vSMTP and open a connexion on port 25.

```sh
$> sudo systemd restart vsmtp
$> telnet 192.168.1.254:25
220 doe-family.com Service ready
554 permanent problems with the remote server
```