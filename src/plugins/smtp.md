# SMTP

The SMTP plugin enables vSMTP to interact with a third party software using the SMTP protocol.
Paired with the `delegate` directive, an incoming email can be delegated to another service via the SMTP protocol.

> This is a native plugin, thus using the `smtp` function does not require an `import` statement.

## Using the plugin

This plugin exposes a single constructor function.

```rust,ignore
export const clamsmtpd = smtp(#{
    delegator: #{
        // The service address to delegate to.
        address: "127.0.0.1:10026",
        // The time allowed between each message before timeout.
        timeout: "2s",
    },
    // The address where vsmtp will gather the results of the delegation.
    // The third party software should be configured to send the email back at this address.
    receiver: "127.0.0.1:10024",
});
```

## Example

The SMTP plugin must be paired with a `delegation` directive.

```rust,ignore
export const clamsmtpd = smtp(#{
    delegator: #{
        address: "127.0.0.1:10026",
        timeout: "2s",
    },
    receiver: "127.0.0.1:10024",
});
```

```rust,ignore
import "service/smtp" as smtp;

#{
    postq: [
        // this will delegate the email using the `clamsmtpd` service.
        delegate smtp::clamsmtpd "delegate antivirus processing" || {
            // this is executed after the delegation results have been
            // received on port 10024.

            // ...
        }
    ]
}
```

> Check the [Delegation](../../filtering/delegation.md) chapter to get more information on the `delegate` directive.
