# Security
## This module contains multiple security functions that you can use to protect your server.

<div style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 20px; border-radius: 5px;'>
<h1> fn <em style='color: var(--inline-code-color);'>check_mail_relay</em>(<em style='color: var(--inline-code-color)'>allowed_hosts</em>) </h1>
 Do not accept a message from a known internal domain if the client is unknown.

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

</div>
<br/>
<br/>

<div style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 20px; border-radius: 5px;'>
<h1> fn <em style='color: var(--inline-code-color);'>check_rcpt_relay</em>(<em style='color: var(--inline-code-color)'>allowed_hosts</em>) </h1>
 Do not accept open relaying.

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

</div>
<br/>
<br/>

<div style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 20px; border-radius: 5px;'>
<h1> fn <em style='color: var(--inline-code-color);'>check_spf</em>(<em style='color: var(--inline-code-color)'>header</em>) </h1>
 Check spf record following the Sender Policy Framework (RFC 7208).
 A wrapper with the policy set to "strict" by default.
 see https://datatracker.ietf.org/doc/html/rfc7208

 # Args

 * `header` - "spf" | "auth" | "both" | "none"

 # Return
 * `deny(code550_7_23 | code451_7_24 | code550_7_24)` - an error occurred during lookup. (returned even when a softfail is received using the "strict" policy)
 * `next()` - the operation succeeded.

 # Effective smtp stage
 `rcpt` and onwards.

 # Errors
 * The `header` argument is not valid.
 * The `policy` argument is not valid.

 # Note
 `check_spf` only checks for the sender's identity, not the `helo` value.

 # Example
 ```js
 #{
     mail: [
        rule "check spf relay" || check_spf(allowed_hosts),
     ]
 }

 #{
     mail: [
         // if this check succeed, it wil return `next`.
         // if it fails, it might return `deny` with a custom code
         // (X.7.24 or X.7.25 for example)
         //
         // if you want to use the return status, just put the check_spf
         // function on the last line of your rule.
         rule "check spf 1" || {
             log("debug", `running sender policy framework on ${ctx().mail_from} identity ...`);
             check_spf("spf", "soft")
         },

         // policy is set to "strict" by default.
         rule "check spf 2" || check_spf("both"),
     ],
 }
 ```
 

</div>
<br/>
<br/>

<div style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 20px; border-radius: 5px;'>
<h1> fn <em style='color: var(--inline-code-color);'>check_spf</em>(<em style='color: var(--inline-code-color)'>header</em>, <em style='color: var(--inline-code-color)'>policy</em>) </h1>
 Check spf record following the Sender Policy Framework (RFC 7208).
 see https://datatracker.ietf.org/doc/html/rfc7208

 # Args

 * `header` - "spf" | "auth" | "both" | "none"
 * `policy` - "strict" | "soft"

 # Return
 * `deny(code550_7_23 | code451_7_24 | code550_7_24)` - an error occurred during lookup. (returned even when a softfail is received using the "strict" policy)
 * `next()` - the operation succeeded.

 # Effective smtp stage
 `rcpt` and onwards.

 # Errors
 * The `header` argument is not valid.
 * The `policy` argument is not valid.

 # Note
 `check_spf` only checks for the sender's identity, not the `helo` value.

 # Example
 ```js
 #{
     mail: [
        rule "check spf" || check_spf("spf", "soft")
     ]
 }

 #{
     mail: [
         // if this check succeed, it wil return `next`.
         // if it fails, it might return `deny` with a custom code
         // (X.7.24 or X.7.25 for example)
         //
         // if you want to use the return status, just put the check_spf
         // function on the last line of your rule.
         rule "check spf 1" || {
             log("debug", `running sender policy framework on ${ctx().mail_from} identity ...`);
             check_spf("spf", "soft")
         },

         // policy is set to "strict" by default.
         rule "check spf 2" || check_spf("both"),
     ],
 }
 ```

 

</div>
<br/>
<br/>

<div style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 20px; border-radius: 5px;'>
<h1> fn <em style='color: var(--inline-code-color);'>sys_check_spf</em>() </h1>
 WARNING: This is a low level api.

 Get spf record following the Sender Policy Framework (RFC 7208).
 see https://datatracker.ietf.org/doc/html/rfc7208

 # Return
 * a rhai `Map`
     * result (String) : the result of an SPF evaluation.
     * cause  (String) : the "mechanism" that matched or the "problem" error (RFC 7208-9.1).

 # Effective smtp stage
 `rcpt` and onwards.

 # Note
 `check_spf` only checks for the sender's identity, not the `helo` value.

 # Example
 ```js
 #{
     mail: [
         rule "raw check spf" || {
             let query = sys_check_spf();

             log("debug", `result: ${query.result}`);

             // the 'result' parameter gives you the result of evaluation.
             // (see https://datatracker.ietf.org/doc/html/rfc7208#section-2.6)
             switch query.result {
                 "pass" => next(),
                 "fail" => {
                     // the 'cause' parameter gives you the cause of the result if there
                     // was an error, and the mechanism of the result if it succeeded.
                     log("error", `check spf error: ${query.cause}`);
                     deny()
                 },
                 _ => next(),
             };
         },
     ],
 }
 ```

 

</div>
<br/>
<br/>

<div style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 20px; border-radius: 5px;'>
<h1> fn <em style='color: var(--inline-code-color);'>verify_dkim</em>() </h1>
 Verify the `DKIM-Signature` header(s) in the mail and produce a `Authentication-Results`.
 see https://datatracker.ietf.org/doc/html/rfc6376

 # Return
 * `accept()` - a signature was successfully verified.
 * `deny()` - no signature could be verified.

 

</div>
<br/>
<br/>