# Adding an antivirus

Malware remains a scourge. As John is aware of security issues, he decides to add a layer of antivirus directly on the MTA. He installed [ClamAV](https://www.clamav.net/) which comes with the [clamsmtpd](https://linux.die.net/man/8/clamsmtpd) antivirus daemon.

## vSMTP security delegation

vSMTP support security delegation via the SMTP protocol (all the logics is defined in `.vsl`):

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

## ClamAV setup

The following example assumes that the `clamsmtpd` service is loaded and started with the following configuration:

```toml
## -- /etc/clamsmtpd.conf

# The address to send scanned mail to.
# This option is required unless TransparentProxy is enabled
OutAddress: 10025

# Address to listen on (defaults to all local addresses on port 10025)
Listen: 127.0.0.1:10026

# Tells clamav to forward the email to vsmtp
# event thought it found a virus. (it drops the email by default)
Action: pass
```

Use the following commands to start clamav:

```shell
sudo systemctl start clamsmtp
sudo systemctl start clamav-daemon
```

## The service

Let's create a `smtp` service in the `/etc/vsmtp/services/smtp.vsl` file:

```js
export const clamsmtpd = smtp(#{
  delegator: #{
    address: "127.0.0.1:10026",
    timeout: "60s",
  },
  receiver: "127.0.0.1:10025",
});
```

The receiver's socket must be enabled in the root config.

```js
fn on_config(config) {
  config.server.interfaces = #{
    //     clients             delegation results
    addr: ["192.168.1.254:25", "127.0.0.1:10025"],
  };

  config
}
```

<p style="text-align: center;"> <i>/etc/vsmtp/conf.d/config.vsl</i> </p>

## The delegate keyword

Create the antivirus passthrough using the `delegate` keyword. As `rule` and `action`, it is a directive that is used to filter emails. The quirk of `delegate` is that it uses a smtp service to delegate the email to a third party software, and get it back on the `receiver` address.

> Check out the [Delegation](../../filtering/delegation.md) chapter for more details.

```js
import "services/smtp" as smtp;

#{
  postq: [
    delegate smtp::clamsmtpd "check email for virus" || {
      // this is executed once the delegation result are received.
      log("debug", "email analyzed by clamsmtpd.");

      // ClamAV inserts the "X-Virus-Infected" header if it founds a virus.
      if has_header("X-Virus-Infected") {
        quarantine("virus_queue")
      } else {
        next()
      }
    }
  ],
}
```

<p style="text-align: center;"> <i>/etc/vsmtp/domain-available/doe-family.com/incoming.vsl</i> </p>

Once the `check email for virus` directive is run, vSMTP will send the email to the `clamsmtpd` service and the rule evaluation is on hold. Once all results are received on the delegation port (10025), evaluation resumes, and the body of this rule is evaluated.

Compromised emails are quarantined in the `virus_queue` folder.
