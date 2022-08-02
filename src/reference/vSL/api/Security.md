# Security
## This module contains multiple security functions that you can use to protect your server.
<details><summary>check_mail_relay(allowed_hosts)</summary><br/> Do not accept a message from a known internal domain if the client is unknown.

 # Args
 * `allowed_hosts` - group of IPv4 | IPv6 | IPv4 range | IPv6 range | fqdn

 # Return
 * `deny()`
 * `next()`

 # Effective smtp stage
 `mail` and onwards.

 # Example
 ```js
 mail: [
    rule "check mail relay" || {
        object allowed_hosts group = [
            object mta_ip ip4 = "192.168.1.254",
            object mta_fqdn fqdn = "mta-internal.foobar.com"
        ];
        check_mail_relay(allowed_hosts)
    }
 ]

 
 ```
</details>
<details><summary>check_rcpt_relay(allowed_hosts)</summary><br/> Do not accept open relaying.

 # Args

 * `allowed_hosts` - group of IPv4 | IPv6 | IPv4 range | IPv6 range | fqdn

 # Return
 * `deny()`
 * `next()`

 # Effective smtp stage
 `rcpt` only.

 # Example
 ```js
 rcpt: [
    rule "check rcpt relay" || {
        object allowed_hosts group = [
            object mta_ip ip4 = "192.168.1.254",
            object mta_fqdn fqdn = "mta-internal.foobar.com"
        ];
        check_rcpt_relay(allowed_hosts)
    }
 ]

 
 ```
</details>
<details><summary>check_spf(header)</summary><br/> Check spf record following the Sender Policy Framework (RFC 7208).
 A wrapper with the policy set to "strict" by default.
 see https://datatracker.ietf.org/doc/html/rfc7208

 # Args

 * `header` - "spf" | "auth" | "both" | "none"

 # Return
 * `deny(code550_7_23 | code451_7_24 | code550_7_24)` - an error occured during lookup. (returned even when a softfail is received using the "strict" policy)
 * `next()` - the operation succeded.

 # Effective smtp stage
 `rcpt` and onwards.

 # Errors
 * The `header` argument is not valid.
 * The `policy` argument is not valid.

 # Example
 ```js
 #{
     rcpt: [
        rule "check spf relay" || check_spf(allowed_hosts),
     ]
 }

 
 ```
</details>
<details><summary>check_spf(header, policy)</summary><br/> Check spf record following the Sender Policy Framework (RFC 7208).
 see https://datatracker.ietf.org/doc/html/rfc7208

 # Args

 * `header` - "spf" | "auth" | "both" | "none"
 * `policy` - "strict" | "soft"

 # Return
 * `deny(code550_7_23 | code451_7_24 | code550_7_24)` - an error occured during lookup. (returned even when a softfail is received using the "strict" policy)
 * `next()` - the operation succeded.

 # Errors
 * The `header` argument is not valid.
 * The `policy` argument is not valid.

 # Effective smtp stage
 `rcpt` and onwards.

 # Example
 ```js
 #{
     rcpt: [
        rule "check spf" || check_spf("spf", "soft")
     ]
 }

 
 ```
</details>
<details><summary>dkim_verify()</summary><br/> Verify the `DKIM-Signature` header(s) in the mail and produce a `Authentication-Results`.
 see https://datatracker.ietf.org/doc/html/rfc6376

 # Return
 * `accept()` - a signature was successfuly verified.
 * `deny()` - no signature could be verified.

 
</details>