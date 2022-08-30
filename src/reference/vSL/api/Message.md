# Message
## Those methods are used to query data from the email and/or mutate it.

<div style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 20px; border-radius: 5px;'>
<h1> fn <em style='color: var(--inline-code-color);'>add_rcpt_message</em>(<em style='color: var(--inline-code-color)'>addr</em>) </h1>
 Add a recipient to the `To` header of the message.

 # Args

 * `addr` - the recipient address to add to the `To` header.

 # Effective smtp stage

 `preq` and onwards.

 # Example
 ```js
 #{
     preq: [
        action "update recipients" || add_rcpt_message("john.doe@example.com"),
     ]
 }
 ```

 

</div>
<br/>
<br/>

<div style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 20px; border-radius: 5px;'>
<h1> fn <em style='color: var(--inline-code-color);'>append_header</em>(<em style='color: var(--inline-code-color)'>header</em>, <em style='color: var(--inline-code-color)'>value</em>) </h1>
 Add a new header at the end of the header list in the message.

 # Args

 * `header` - the name of the header to append.
 * `value` - the value of the header to append.

 # Effective smtp stage

 All of them. Even though the email is not received at the current stage,
 vsmtp stores new headers and will add them on top of the ones received once
 the `preq` stage is reached.

 # Example
 ```js
 #{
     postq: [
         action "append a header" || {
             append_header("X-JOHN", "received by john's server.");
         }
     ],
 }
 ```

 

</div>
<br/>
<br/>

<div style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 20px; border-radius: 5px;'>
<h1> fn <em style='color: var(--inline-code-color);'>get_domain</em>() </h1>
 Get the domain of an email address.

 # Args

 * `address` - the address to extract the domain from.

 # Effective smtp stage

 All of them.

 # Example
 ```js
 #{
     mail: [
         // You can also use the `get_domain(mail_from())` syntax.
         action "display sender's domain" || {
             log("info", `received a message from domain ${mail_from().domain}.`);
         }
     ],
 }
 ```

 

</div>
<br/>
<br/>

<div style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 20px; border-radius: 5px;'>
<h1> fn <em style='color: var(--inline-code-color);'>get_domains</em>() </h1>
 Get all domains of the recipient list.

 # Args

 * `rcpt_list` - the recipient list.

 # Effective smtp stage

 `mail` and onwards.

 # Example
 ```js
 #{
     mail: [
         action "display recipients domains" || {
             print("list of recipients domains:");

             // You can also use the `get_domains(rcpt_list())` syntax.
             for domain in rcpt_list().domains {
                 print(`- ${domain}`);
             }
         }
     ],
 }
 ```

 

</div>
<br/>
<br/>

<div style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 20px; border-radius: 5px;'>
<h1> fn <em style='color: var(--inline-code-color);'>get_header</em>(<em style='color: var(--inline-code-color)'>header</em>) </h1>
 Get a specific header from the incoming message.

 # Args

 * `header` - the name of the header to get.

 # Return

 * `string` - the header value, or an empty string if the header was not found.

 # Effective smtp stage

 `preq` and onwards.

 # Example
 ```js
 #{
     postq: [
         action "display VSMTP header" || {
             print(get_header("X-VSMTP"));
         }
     ],
 }
 ```

 

</div>
<br/>
<br/>

<div style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 20px; border-radius: 5px;'>
<h1> fn <em style='color: var(--inline-code-color);'>get_local_part</em>() </h1>
 Get the local part of an email address.

 # Args

 * `address` - the address to extract the local part from.

 # Effective smtp stage

 All of them.

 # Example
 ```js
 #{
     mail: [
         // You can also use the `get_local_part(mail_from())` syntax.
         action "display mail from identity" || {
             log("info", `received a message from ${mail_from().local_part}.`);
         }
     ],
 }
 ```

 

</div>
<br/>
<br/>

<div style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 20px; border-radius: 5px;'>
<h1> fn <em style='color: var(--inline-code-color);'>get_local_parts</em>() </h1>
 Get all local parts of the recipient list.

 # Args

 * `rcpt_list` - the recipient list.

 # Effective smtp stage

 `mail` and onwards.

 # Example
 ```js
 #{
     mail: [
         action "display recipients usernames" || {
             print("list of recipients user names:");

             // You can also use the `get_local_parts(rcpt_list())` syntax.
             for user in rcpt_list().local_parts {
                 print(`- ${user}`);
             }
         }
     ],
 }
 ```

 

</div>
<br/>
<br/>

<div style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 20px; border-radius: 5px;'>
<h1> fn <em style='color: var(--inline-code-color);'>has_header</em>(<em style='color: var(--inline-code-color)'>header</em>) </h1>
 Checks if the message contains a specific header.

 # Args

 * `header` - the name of the header to search.

 # Effective smtp stage

 `preq` and onwards.

 # Example
 ```js
 #{
     postq: [
         action "check for VSMTP header" || {
             if has_header("X-VSMTP") {
                 log("info", "incoming message could be from another vsmtp server");
             }
         }
     ],
 }
 ```

 

</div>
<br/>
<br/>

<div style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 20px; border-radius: 5px;'>
<h1> fn <em style='color: var(--inline-code-color);'>mail</em>() </h1>
 Get a copy of the whole email as a string.

 # Effective smtp stage

 `preq` and onwards.

 # Example
 ```js
 #{
     postq: [
        action "display email content" || log("trace", `email content: ${mail()}`),
     ]
 }
 ```

 

</div>
<br/>
<br/>

<div style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 20px; border-radius: 5px;'>
<h1> fn <em style='color: var(--inline-code-color);'>prepend_header</em>(<em style='color: var(--inline-code-color)'>header</em>, <em style='color: var(--inline-code-color)'>value</em>) </h1>
 Add a new header on top all other headers in the message.

 # Args

 * `header` - the name of the header to prepend.
 * `value` - the value of the header to prepend.

 # Effective smtp stage

 All of them. Even though the email is not received at the current stage,
 vsmtp stores new headers and will add them on top of the ones received once
 the `preq` stage is reached.

 # Example
 ```js
 #{
     postq: [
         action "prepend a header" || {
             prepend_header("X-JOHN", "received by john's server.");
         }
     ],
 }
 ```

 

</div>
<br/>
<br/>

<div style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 20px; border-radius: 5px;'>
<h1> fn <em style='color: var(--inline-code-color);'>remove_rcpt_message</em>(<em style='color: var(--inline-code-color)'>addr</em>) </h1>
 Remove a recipient from the `To` header of the message.

 # Args

 * `addr` - the recipient to remove to the `To` header.

 # Effective smtp stage

 `preq` and onwards.

 # Example
 ```js
 #{
     preq: [
        action "update recipients" || remove_rcpt_message("john.doe@example.com"),
     ]
 }
 ```

 

</div>
<br/>
<br/>

<div style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 20px; border-radius: 5px;'>
<h1> fn <em style='color: var(--inline-code-color);'>rewrite_mail_from_message</em>(<em style='color: var(--inline-code-color)'>new_addr</em>) </h1>
 Change the sender's address in the `From` header of the message.

 # Args

 * `new_addr` - the new sender address to set.

 # Effective smtp stage

 `preq` and onwards.

 # Example
 ```js
 #{
     preq: [
        action "replace sender" || rewrite_mail_from_message("john.server@example.com"),
     ]
 }
 ```

 

</div>
<br/>
<br/>

<div style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 20px; border-radius: 5px;'>
<h1> fn <em style='color: var(--inline-code-color);'>rewrite_rcpt_message</em>(<em style='color: var(--inline-code-color)'>old_addr</em>, <em style='color: var(--inline-code-color)'>new_addr</em>) </h1>
 Replace a recipient by an other in the `To` header of the message.

 # Args

 * `old_addr` - the recipient to replace.
 * `new_addr` - the new address to use when replacing `old_addr`.

 # Effective smtp stage

 `preq` and onwards.

 # Example
 ```js
 #{
     preq: [
        action "rewrite recipient" || rewrite_rcpt_message("john.doe@example.com", "john-mta@example.com"),
     ]
 }
 ```

 

</div>
<br/>
<br/>

<div style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 20px; border-radius: 5px;'>
<h1> fn <em style='color: var(--inline-code-color);'>set_header</em>(<em style='color: var(--inline-code-color)'>header</em>, <em style='color: var(--inline-code-color)'>value</em>) </h1>
 Replace an existing header value by a new value, or append a new header
 to the message.

 # Args

 * `header` - the name of the header to set or add.
 * `value` - the value of the header to set or add.

 # Effective smtp stage

 All of them. Even though the email is not received at the current stage,
 vsmtp stores new headers and will add them on top to the ones received once
 the `preq` stage is reached.

 Be aware that if you want to set a header value from the original message,
 you must use `set_header` in the `preq` stage and onwards.

 # Example
 ```js
 #{
     postq: [
         action "update subject" || {
             let subject = get_header("Subject");
             set_header("Subject", `${subject} (analyzed by vsmtp)`);
         }
     ],
 }
 ```

 

</div>
<br/>
<br/>