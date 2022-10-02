# Status
The state of an SMTP transaction can be changed through specific functions from this module.

<div style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 20px; border-radius: 5px;'>
<h2> fn <em style='color: var(--inline-code-color);'>accept</em>() </h2>
 Tell the rule engine to accept the incoming transaction for the current stage.
 This means that all rules following the one `accept` is called in the current stage
 will be ignored.

 ### Effective smtp stage

 all of them.

 ### Example
 ```js
 #{
     connect: [
         // "ignored checks" will be ignored because the previous rule returned accept.
         rule "accept" || accept(),
         action "ignore checks" || print("this will be ignored because the previous rule used accept()."),
     ],

     mail: [
         // rule evaluation is resumed in the next stage.
         rule "resume rules" || print("evaluation resumed!");
     ]
 }
 ```

 

</div>
<br/>
<br/>

<div style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 20px; border-radius: 5px;'>
<h2> fn <em style='color: var(--inline-code-color);'>deny</em>() </h2>
 Stop rules evaluation and/or send an error code to the client.
 The code sent is `554 - permanent problems with the remote server`.

 ### Effective smtp stage

 all of them.

 ### Example
 ```js
 #{
     rcpt: [
         rule "check for satan" || {
            // The client is denied if a recipient's domain matches satan.org,
            // this is a blacklist, sort-of.
            if rcpt().domain == "satan.org" {
                deny()
            } else {
                next()
            }
        },
     ],
 }
 ```

 

</div>
<br/>
<br/>

<div style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 20px; border-radius: 5px;'>
<h2> fn <em style='color: var(--inline-code-color);'>deny</em>(<em style='color: var(--inline-code-color)'>code</em>) </h2>
 Stop rules evaluation and/or send a custom code to the client.

 ### Effective smtp stage

 all of them.

 ### Example
 ```js
 #{
     rcpt: [
         rule "check for satan" || {
            // a custom error code can be used with `deny`.
            const error_code = code(550, "satan.org is not welcome here.");

            // The client is denied if a recipient's domain matches satan.org,
            // this is a blacklist, sort-of.
            if rcpt().domain == "satan.org" {
                deny(error_code)
            } else {
                next()
            }
        },
     ],
 }
 ```

 

</div>
<br/>
<br/>

<div style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 20px; border-radius: 5px;'>
<h2> fn <em style='color: var(--inline-code-color);'>faccept</em>() </h2>
 Tell the rule engine to force accept the incoming transaction.
 This means that all rules following the one `faccept` is called
 will be ignored.

 Use this return status when you are sure that
 the incoming client can be trusted.

 ### Effective smtp stage

 all of them.

 ### Example
 ```js
 #{
     connect: [
         // Here we imagine that "192.168.1.10" is a trusted source, so we can force accept
         // any other rules that don't need to be run.
         rule "check for trusted source" || if client_ip() == "192.168.1.10" { faccept() } else { next() },
     ],

     // The following rules will not be evaluated if `client_ip() == "192.168.1.10"` is true.
     mail: [
         rule "another rule" || {
             // ... doing stuff
         }
     ],
 }

 
 ```

</div>
<br/>
<br/>

<div style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 20px; border-radius: 5px;'>
<h2> fn <em style='color: var(--inline-code-color);'>info</em>(<em style='color: var(--inline-code-color)'>code</em>) </h2>
 Ask the client to retry to send the current command by sending an information code.

 ### Effective smtp stage

 all of them.

 ### Example
 ```js
 #{
     connect: [
         rule "please retry" || {
            const info_code = code(451, "failed to understand you request, please retry.");
            info(info_code)
        },
     ],
 }
 ```

 

</div>
<br/>
<br/>

<div style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 20px; border-radius: 5px;'>
<h2> fn <em style='color: var(--inline-code-color);'>next</em>() </h2>
 Tell the rule engine that a rule succeeded.

 ### Effective smtp stage

 all of them.

 ### Example
 ```js
 #{
     connect: [
         // once "go to the next rule" is evaluated, the rule engine execute "another rule".
         rule "go to the next rule" || next(),
         action "another rule" || print("checking stuff ..."),
     ],
 }
 ```

 

</div>
<br/>
<br/>

<div style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 20px; border-radius: 5px;'>
<h2> fn <em style='color: var(--inline-code-color);'>quarantine</em>(<em style='color: var(--inline-code-color)'>queue</em>) </h2>
 Skip all rules until the email is received and place the email in a
 quarantine queue.

 ### Args

 * `queue` - the relative path to the queue where the email will be quarantined. This path will be concatenated to the [app.dirpath] field in your `vsmtp.toml`.

 ### Effective smtp stage

 all of them.

 ### Example
 ```js
 import "services" as svc;

 #{
     postq: [
           delegate svc::clamsmtpd "check email for virus" || {
               // the email is placed in quarantined if a virus is detected by
               // a service.
               if has_header("X-Virus-Infected") {
                 quarantine("virus_queue")
               } else {
                 next()
               }
           }
     ],
 }
 ```

 

</div>
<br/>
<br/>