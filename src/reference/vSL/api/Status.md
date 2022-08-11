# Status
## The state of an SMTP transaction can be changed through specific functions from this module.
<details>
<summary>
<code>
accept()
</code>
</summary>
<br/>
<div style='padding: 10px; border-radius: 5px; border-style: solid; border-color: white'>
 Tell the rule engine to accept the incomming transaction for the current stage.
 This means that all rules following the one `accept` is called in the current stage
 will be ignored.

 # Effective smtp stage

 all of them.

 # Example
 ```js
 #{
     connect: [
         // "ignored checks" will be ignored because the previous rule returned accept.
         rule "accept" || accept(),
         rule "ignored checks" || print("this will be ignored.")
     ],

     mail: [
         // rule evaluation is resumed in the next stage.
         rule "resuming rules" || print("we resume rule evaluation here.");
     ]
 }
 ```

 

</div>
<br/>
</details>
<details>
<summary>
<code>
deny()
</code>
</summary>
<br/>
<div style='padding: 10px; border-radius: 5px; border-style: solid; border-color: white'>
 Stop rules evaluation and/or send an error code to the client.
 The code sent is `554 - permanent problems with the remote server`.

 # Effective smtp stage

 all of them.

 # Example
 ```js
 #{
     rcpt: [
         rule "" || {
            // The client is denied if a recipient's domain matches satan.org,
            // this is a blacklist, sort-of.
            if ctx().rcpt.domain == "satan.org" {
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
</details>
<details>
<summary>
<code>
deny(code)
</code>
</summary>
<br/>
<div style='padding: 10px; border-radius: 5px; border-style: solid; border-color: white'>
 Stop rules evaluation and/or send a custom code to the client.

 # Effective smtp stage

 all of them.

 # Example
 ```js
 #{
     rcpt: [
         rule "" || {
            // a custom error code can be used with `deny`.
            object error_code code = #{ code: 550, enhanced: "", text: "satan.org is not welcome here." };

            // The client is denied if a recipient's domain matches satan.org,
            // this is a blacklist, sort-of.
            if ctx().rcpt.domain == "satan.org" {
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
</details>
<details>
<summary>
<code>
faccept()
</code>
</summary>
<br/>
<div style='padding: 10px; border-radius: 5px; border-style: solid; border-color: white'>
 Tell the rule engine to force accept the incomming transaction.
 This means that all rules following the one `faccept` is called
 will be ignored.

 Use this return status when you are sure that
 the incoming client can be trusted.

 # Effective smtp stage

 all of them.

 # Example
 ```js
 #{
     connect: [
         // Here we imagine that "192.168.1.10" is a trusted source, so we can force accept
         // any other rules that don't need to be run.
         rule "check for trusted source" || if client_ip() == "192.168.1.10" { faccept() } else { next() },
     ],
 }

 
 ```

</div>
<br/>
</details>
<details>
<summary>
<code>
info(code)
</code>
</summary>
<br/>
<div style='padding: 10px; border-radius: 5px; border-style: solid; border-color: white'>
 Ask the client to retry to send the current comment by sending an information code.

 # Effective smtp stage

 all of them.

 # Example
 ```js
 #{
     connect: [
         rule "" || {
            object info_code code = #{ code: 451, enhanced: "", text: "failed to understand you request, please retry." };
            info(info_code)
        },
     ],
 }
 ```

 

</div>
<br/>
</details>
<details>
<summary>
<code>
next()
</code>
</summary>
<br/>
<div style='padding: 10px; border-radius: 5px; border-style: solid; border-color: white'>
 Tell the rule engine that a rule succeeded.

 # Effective smtp stage

 all of them.

 # Example
 ```js
 #{
     connect: [
         // once "go next" is evaluated, the rule engine execute "another rule".
         rule "go next" || next(),
         rule "another rule" || print("checking stuff ..."),
     ],
 }
 ```

 

</div>
<br/>
</details>
<details>
<summary>
<code>
quarantine(queue)
</code>
</summary>
<br/>
<div style='padding: 10px; border-radius: 5px; border-style: solid; border-color: white'>
 Skip all rules until the email is received and place the email in a
 quarantine queue.

 # Args

 * `queue` - the relative path to the queue where the email will be quarantined.

 # Effective smtp stage

 all of them.

 # Example
 ```js
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
</details>