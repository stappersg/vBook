# SMTP security delegation

vSMTP support security delegation via the SMTP protocol and vsl's configuration.
In the next example, we are going to configure vsmtp to delegate emails to the
[clamsmtpd antivirus daemon](https://linux.die.net/man/8/clamsmtpd).

## The service

First off, create a smtp service in vsl like so:

```rust
// -- antivirus.vsl
service clamsmtpd smtp = #{
    // the service will send messages to "127.0.0.1:10026".
    delegator: #{
        address: "127.0.0.1:10026",
        timeout: "60s",
    },
    // the service will receive delegation results on "127.0.0.1:10024".
    receiver: "127.0.0.1:10024",
};
```

In the toml configuration, you need to enable the receiver's socket.

```toml
# -- vsmtp.toml
version_requirement = ">=1.0.0"

[server.interfaces]
#      clients             delegation results
addr = ["127.0.0.1:10025", "127.0.0.1:10024"]
addr_submission = ["127.0.0.1:10587"]
addr_submissions = ["127.0.0.1:10465"]
```

## Rules

You service is configured. Now, to use it, create the following rule using the `delegate` keyword.

```rust
// -- main.vsl
import "antivirus" as antivirus;

#{
    preq: [
        /// once this rule is run, vsmtp will send the email to the
        /// clamsmtpd service and rule evaluation will be on hold.
        /// once all results are received on the 10024 port, evaluation
        /// will resume, and the body of this rule will be evaluated.
        delegate antivirus::clamsmtpd "check email for virus" || {
            // this is executed once the delegation result are received.
            log("debug", "email analyzed.");
            log("trace", `content: ${msg().mail}`);

            // check if X-CLAMAV header is found ...
            // set email in quarantine if it is compromised ...
            next()
        }
    ],
}
```

## That's it

Any service that supports the SMTP protocol can be used to delegate the email
processing / security with the `delegate` rule.