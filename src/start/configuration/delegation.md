# SMTP security delegation

## Adding an antivirus

Malware remains a scourge. As John is aware of security issues, he decides to add a layer of antivirus directly on the MTA. He installed [ClamAV](https://www.clamav.net/) which comes with the [clamsmtpd antivirus daemon](https://linux.die.net/man/8/clamsmtpd).

```console
{ Incomming msg } ---> vSMTP server ---> { Delivered msg }
                        |       ^
                        |       |
         clamAV socket  |       | vSMTP socket
         (delegator)    |       | (receiver)
       127.0.0.1:10026  |       | 127.0.0.1:10025
                        |       |
                        v       |
                  { clamsmtpd daemon } <-> { clamAV }
```

vSMTP support security delegation via the SMTP protocol. Configuration is done for the system part in the vsmtp.toml file, and for the application part in the main.vsl file.

## Clamav setup

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

Create a smtp service in vsl:

```javascript
// -- service.vsl
service clamsmtpd smtp = #{
    delegator: #{
        address: "127.0.0.1:10026",
        timeout: "60s",
    },
    receiver: "127.0.0.1:10025",
};
```

The the receiver's socket must be enabled in the toml configuration file.

```toml
# -- vsmtp.toml
[server.interfaces]
#      clients             delegation results
addr = ["192.168.1.254:25", "127.0.0.1:10025"]
```

## Rules

Create the antivirus passthrough using the `delegate` keyword. Any service that supports the SMTP protocol can be used.

```javascript
// -- main.vsl
// You cannot use `import "service" as service;` here because `service` is
// a reserved keyword.
import "service" as svc;

#{
    postq: [
        // a `delegate` directive is like a `rule`, it needs
        // to return a status code. The difference is that it
        // first sends the content of the mail to the service
        // via the smtp protocol and then execute its body.
        delegate svc::clamsmtpd "check email for virus" || {
            // this is executed once the delegation result are received.
            log("debug", "email analyzed.");

            // clamav inserts the "X-Virus-Infected" header
            // once a virus is detected, we juste have to
            // check on that.
            if has_header("X-Virus-Infected") {
                quarantine("virus_q")
            } else {
                next()
            }
        }
    ],
}
```

> Since there is no heavy network traffic, John decided to do a post-queue filtering. Compromised emails are quarantined in the `virus_q` folder.

Once the "check email for virus" rule is run, vsmtp will send the email to the clamsmtpd service and rule evaluation is on hold. Once all results are received on the delegation port (10025), evaluation
resumes, and the body of this rule is evaluated.

___That's all folks !___
