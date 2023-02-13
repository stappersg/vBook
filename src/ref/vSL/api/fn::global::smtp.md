# global::smtp


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> connect </h2>

```rust,ignore
fn connect(parameters: Map) -> Smtp
```

<details>
<summary markdown="span"> details </summary>

Connect to a third party software that accepts SMTP transactions.
This module is used with the `delegate` keyword.

# Args

* `parameters` - a map of the following parameters:
    * `delegator` - a map of the following parameters.
        * `address` - the address to connect to the third-party software
        * `timeout` - timeout between each SMTP commands. (optional, default: 30s)
    * `receiver` - the socket to get back the result from.

# Return

A service used to delegate a message.

# Error

* The service failed to parse the command parameters.
* The service failed to connect to the `delegator` address.

# Example

```text
// declared in /etc/vsmtp/services/smtp.vsl
export const clamsmtpd = smtp::connect(#{
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

The service is then used in a rule file using the following syntax:

```text
import "service/smtp" as srv;

#{
    postq: [
        // this will delegate the email using the `clamsmtpd` service.
        delegate srv::clamsmtpd "delegate antivirus processing" || {
            // this is executed after the delegation results have been
            // received on port 10024.
        }
    ]
}
```
</details>

</div>
</br>
