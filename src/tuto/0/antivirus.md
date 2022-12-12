# Adding an antivirus

<!-- markdown-link-check-disable-next-line -->
Malware remains a scourge. As John is aware of security issues, he decides to add a layer of antivirus directly on the MTA. He installed [ClamAV](https://www.clamav.net/) which comes with the [clamsmtpd](https://linux.die.net/man/8/clamsmtpd) antivirus daemon.

vSMTP support security delegation via the SMTP protocol using `.vsl` scripts. In the following tutorial, we are going to setup a delegation workflow that looks like the following.

```txt
{ Incoming msg }  ---> vSMTP server ---> { Delivered msg }
                        |       ^
                        |       |
      clamsmtpd socket  |       |   vSMTP socket
         (delegator)    |       |    (receiver)
       127.0.0.1:10026  |       |  127.0.0.1:10025
                        |       |
                        v       |
                  { clamsmtpd daemon } <-> { ClamAV }
```
<p class="ann"> Delegating emails to clamav and getting back the results </p>

## ClamAV setup

The following example assumes that the `clamsmtpd` service is loaded and started with the following configuration:

```toml
# The address to send scanned mail to.
# This option is required unless TransparentProxy is enabled
OutAddress: 10025

# Address to listen on (defaults to all local addresses on port 10025)
Listen: 127.0.0.1:10026

# Tells clamav to forward the email to vsmtp
# event thought it found a virus. (it drops the email by default)
Action: pass
```
<p class="ann"> clamav configuration at `/etc/clamsmtpd.conf` </p>

```shell
sudo systemctl start clamsmtp
sudo systemctl start clamav-daemon
```
<p class="ann"> Starting clamav </p>

## SMTP Service

Let's create a `smtp` service in the `/etc/vsmtp/services/smtp.vsl` script to send incoming emails to clamsmtpd and receive them back on a specific address.

```rust,ignore
export const clamsmtpd = smtp(#{
  delegator: #{
    address: "127.0.0.1:10026",
    timeout: "60s",
  },
  receiver: "127.0.0.1:10025",
});
```
<p class="ann"> Declaring a SMTP service </p>

The receiver's socket must be enabled in the root config.

```rust,ignore
fn on_config(config) {
  config.server.interfaces = #{
    addr: [
      // Receiver for clients.
      "192.168.1.254:25",
      // Receiver for delegation results from clamav.
      "127.0.0.1:10025"
    ],
  };

  config
}
```
<p class="ann"> Update the root configuration with a receiver for clamav </p>

## Filtering

Create the antivirus passthrough using the `delegate` keyword in the `/etc/vsmtp/domain-available/doe-family.com/incoming.vsl` script.

```rust,ignore
import "services/smtp" as smtp;

#{
  postq: [
    delegate smtp::clamsmtpd "check email for virus" || {
      // this is executed once the delegation result are received.
      log("debug", "email analyzed by clamsmtpd.");

      // ClamAV inserts the "X-Virus-Infected" header if it found a virus.
      if has_header("X-Virus-Infected") {
        quarantine("virus_queue")
      } else {
        next()
      }
    }
  ],
}
```
<p class="ann"> Moving infected emails in the `virus_queue` quarantine queue. </p>

Compromised emails are quarantined in the `virus_queue` folder.

> Check out the [Delegation](../../filtering/delegation.md) chapter for more details.