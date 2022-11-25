# Security
This module contains multiple security functions that you can use to protect your server.

<div style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 20px; border-radius: 5px;'>
<h2> fn <em style='color: var(--inline-code-color);'>check_dmarc</em>() </h2>
 Apply the DMARC policy to the mail.

 ### Effective smtp stage

 `preq` and onwards.

 ### Example

 ```js
 #{
   preq: [
     rule "check dmarc" || { check_dmarc() },
   ]
 }
 ```

 

</div>
<br/>
<br/>

<div style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 20px; border-radius: 5px;'>
<h2> fn <em style='color: var(--inline-code-color);'>check_mail_relay</em>(<em style='color: var(--inline-code-color)'>allowed_hosts</em>) </h2>
 Do not accept a message from a known internal domain if the client is unknown.

 ### Args
 * `allowed_hosts` - group of IPv4 | IPv6 | IPv4 range | IPv6 range | fqdn

 ### Return
 * `deny()`
 * `next()`

 ### Effective smtp stage
 `mail` and onwards.

 ### Example
 ```js
 mail: [
    rule "check mail relay" || {
        const allowed_hosts = [
            ip4("192.168.1.254"),
            fqdn("mta-internal.foobar.com")
        ];
        check_mail_relay(allowed_hosts)
    }
 ]

 
 ```

</div>
<br/>
<br/>

<div style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 20px; border-radius: 5px;'>
<h2> fn <em style='color: var(--inline-code-color);'>check_rcpt_relay</em>(<em style='color: var(--inline-code-color)'>allowed_hosts</em>) </h2>
 Do not accept open relaying.

 ### Args

 * `allowed_hosts` - group of IPv4 | IPv6 | IPv4 range | IPv6 range | fqdn

 ### Return
 * `deny()`
 * `next()`

 ### Effective smtp stage
 `rcpt` only.

 ### Example
 ```js
 rcpt: [
    rule "check rcpt relay" || {
        const allowed_hosts = [
            ip4("192.168.1.254"),
            fqdn("mta-internal.foobar.com")
        ];
        check_rcpt_relay(allowed_hosts)
    }
 ]

 
 ```

</div>
<br/>
<br/>

<div style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 20px; border-radius: 5px;'>
<h2> fn <em style='color: var(--inline-code-color);'>check_spf</em>(<em style='color: var(--inline-code-color)'>header</em>) </h2>
 Check spf record following the Sender Policy Framework (RFC 7208).
 A wrapper with the policy set to "strict" by default.
 see https://datatracker.ietf.org/doc/html/rfc7208

 ### Args

 * `header` - "spf" | "auth" | "both" | "none"

 ### Return
 * `deny(code550_7_23 | code451_7_24 | code550_7_24)` - an error occurred during lookup. (returned even when a softfail is received using the "strict" policy)
 * `next()` - the operation succeeded.

 ### Effective smtp stage
 `rcpt` and onwards.

 ### Errors
 * The `header` argument is not valid.
 * The `policy` argument is not valid.

 ### Note
 `check_spf` only checks for the sender's identity, not the `helo` value.

 ### Example
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
             log("debug", `running sender policy framework on ${mail_from()} identity ...`);
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
<h2> fn <em style='color: var(--inline-code-color);'>check_spf</em>(<em style='color: var(--inline-code-color)'>header</em>, <em style='color: var(--inline-code-color)'>policy</em>) </h2>
 Check spf record following the Sender Policy Framework (RFC 7208).
 see https://datatracker.ietf.org/doc/html/rfc7208

 ### Args

 * `header` - "spf" | "auth" | "both" | "none"
 * `policy` - "strict" | "soft"

 ### Return
 * `deny(code550_7_23 | code451_7_24 | code550_7_24)` - an error occurred during lookup. (returned even when a softfail is received using the "strict" policy)
 * `next()` - the operation succeeded.

 ### Effective smtp stage
 `rcpt` and onwards.

 ### Errors
 * The `header` argument is not valid.
 * The `policy` argument is not valid.

 ### Note
 `check_spf` only checks for the sender's identity, not the `helo` value.

 ### Example
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
             log("debug", `running sender policy framework on ${mail_from()} identity ...`);
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
<h2> fn <em style='color: var(--inline-code-color);'>check_spf_inner</em>() </h2>
 WARNING: This is a low level api.

 Get spf record following the Sender Policy Framework (RFC 7208).
 see https://datatracker.ietf.org/doc/html/rfc7208

 ### Return
 * a rhai `Map`
     * result (String) : the result of an SPF evaluation.
     * cause  (String) : the "mechanism" that matched or the "problem" error (RFC 7208-9.1).

 ### Effective smtp stage
 `rcpt` and onwards.

 ### Note
 `check_spf` only checks for the sender's identity, not the `helo` value.

 ### Example
 ```js
 #{
     mail: [
         rule "raw check spf" || {
             let query = check_spf_inner();

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
<h2> fn <em style='color: var(--inline-code-color);'>sign_dkim</em>(<em style='color: var(--inline-code-color)'>selector</em>) </h2>
 Alias for `sign_dkim(selector, ["From", "To", "Date", "Subject", "From"], "simple/relaxed")`

 

</div>
<br/>
<br/>

<div style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 20px; border-radius: 5px;'>
<h2> fn <em style='color: var(--inline-code-color);'>sign_dkim</em>(<em style='color: var(--inline-code-color)'>selector</em>, <em style='color: var(--inline-code-color)'>headers_field</em>, <em style='color: var(--inline-code-color)'>canonicalization</em>) </h2>
 Produce a `DKIM-Signature` header.

 ### Args

 * `selector` - the DNS selector to expose the public key & for the verifier
 * `headers_field` - list of headers to sign
 * `canonicalization` - the canonicalization algorithm to use (ex: "simple/relaxed")

 ### Effective smtp stage

 `preq` and onwards.

 ### Example

 ```js
 #{
   preq: [
     action "sign dkim" || {
       sign_dkim("2022-09", ["From", "To", "Date", "Subject", "From"], "simple/relaxed");
     },
   ]
 }
 ```

 

</div>
<br/>
<br/>

<div style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 20px; border-radius: 5px;'>
<h2> fn <em style='color: var(--inline-code-color);'>verify_dkim</em>() </h2>
 Verify the `DKIM-Signature` header(s) in the mail and produce a `Authentication-Results`.
 If this function has already been called once, it will return the result of the previous call.
 see https://datatracker.ietf.org/doc/html/rfc6376

 ### Return

 * a DkimResult object

 ### Effective smtp stage

 `preq` and onwards.

 ### Example

 ```js
 #{
   preq: [
     action "check dkim" || { verify_dkim(); },
   ]
 }
 ````

 

</div>
<br/>
<br/>