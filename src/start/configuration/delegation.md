# SMTP security delegation

## Adding an antivirus

John is aware of security issues. Malware remains a scourge on the internet.
So he decides to add a second layer of antivirus.

Therefore, he installed [ClamAV](https://www.clamav.net/) which comes with the [clamsmtpd antivirus daemon](https://linux.die.net/man/8/clamsmtpd).

vSMTP support security delegation via the SMTP protocol and vsl's configuration. In the next example, we are going to configure vsmtp to delegate emails to `clamsmtpd`.

The following example assumes that you started the `clamsmtpd` service with the following config:

```
# The address to send scanned mail to.
# This option is required unless TransparentProxy is enabled
OutAddress: 10025

# Address to listen on (defaults to all local addresses on port 10025)
Listen: 127.0.0.1:10026
```

## The service

First off, create a smtp service in vsl like so:

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

In the toml configuration, you need to enable the receiver's socket.

```toml
# -- vsmtp.toml
[server.interfaces]
#      clients             delegation results
addr = ["192.168.1.254:25", "127.0.0.1:10025"]
```

## Rules

You service is configured. Now, to use it, create the following rule using the `delegate` keyword.

```javascript
// -- main.vsl
import "service" as service;

#{
    postq: [
        /// once this rule is run, vsmtp will send the email to the
        /// clamsmtpd service and rule evaluation will be on hold.
        /// once all results are received on the 10024 port, evaluation
        /// will resume, and the body of this rule will be evaluated.
        delegate service::clamsmtpd "check email for virus" || {
            // this is executed once the delegation result are received.
            log("debug", "email analyzed.");

            // clamav inserts the "X-Virus-Infected" header
            // once a virus is detected. 
            if has_header("X-Virus-Infected") {
                quarantine("virus_q")
            } else {
                next()
            }
        }
    ],
}
```

Since there is no heavy network traffic, John decided to do a pre-queue filtering.
Compromised emails are quarantined in the `virus_q` folder.

## That's it

Any service that supports the SMTP protocol can be used to delegate the email
processing / security with the `delegate` directive.