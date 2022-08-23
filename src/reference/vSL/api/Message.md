# Message
## Those methods are used to query data from the email and/or mutate it.
<details>
<summary>
<code>
add_rcpt_message(addr)
</code>
</summary>
<br/>
<div style='padding: 10px; border-radius: 5px; border-style: solid; border-color: white'>
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
</details>
<details>
<summary>
<code>
append_header(header, value)
</code>
</summary>
<br/>
<div style='padding: 10px; border-radius: 5px; border-style: solid; border-color: white'>
 Append a new header to the message.

 # Args

 * `header` - the name of the header to append.
 * `value` - the value of the header to append.

 # Effective smtp stage

 All of them. Even tought the email is not received at the current stage,
 vsmtp stores new headers and will prepend them to the ones received once
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
</details>
<details>
<summary>
<code>
get_domain()
</code>
</summary>
<br/>
<div style='padding: 10px; border-radius: 5px; border-style: solid; border-color: white'>
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
</details>
<details>
<summary>
<code>
get_domains()
</code>
</summary>
<br/>
<div style='padding: 10px; border-radius: 5px; border-style: solid; border-color: white'>
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
</details>
<details>
<summary>
<code>
get_header(header)
</code>
</summary>
<br/>
<div style='padding: 10px; border-radius: 5px; border-style: solid; border-color: white'>
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
</details>
<details>
<summary>
<code>
get_local_part()
</code>
</summary>
<br/>
<div style='padding: 10px; border-radius: 5px; border-style: solid; border-color: white'>
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
</details>
<details>
<summary>
<code>
get_local_parts()
</code>
</summary>
<br/>
<div style='padding: 10px; border-radius: 5px; border-style: solid; border-color: white'>
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
</details>
<details>
<summary>
<code>
has_header(header)
</code>
</summary>
<br/>
<div style='padding: 10px; border-radius: 5px; border-style: solid; border-color: white'>
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
</details>
<details>
<summary>
<code>
mail()
</code>
</summary>
<br/>
<div style='padding: 10px; border-radius: 5px; border-style: solid; border-color: white'>
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
</details>
<details>
<summary>
<code>
prepend_header(header, value)
</code>
</summary>
<br/>
<div style='padding: 10px; border-radius: 5px; border-style: solid; border-color: white'>
 Prepend a new header to the message.

 # Args

 * `header` - the name of the header to prepend.
 * `value` - the value of the header to prepend.

 # Effective smtp stage

 All of them. Even tought the email is not received at the current stage,
 vsmtp stores new headers and will prepend them to the ones received once
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
</details>
<details>
<summary>
<code>
remove_rcpt_message(addr)
</code>
</summary>
<br/>
<div style='padding: 10px; border-radius: 5px; border-style: solid; border-color: white'>
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
</details>
<details>
<summary>
<code>
rewrite_mail_from_message(new_addr)
</code>
</summary>
<br/>
<div style='padding: 10px; border-radius: 5px; border-style: solid; border-color: white'>
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
</details>
<details>
<summary>
<code>
rewrite_rcpt_message(old_addr, new_addr)
</code>
</summary>
<br/>
<div style='padding: 10px; border-radius: 5px; border-style: solid; border-color: white'>
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
</details>
<details>
<summary>
<code>
set_header(header, value)
</code>
</summary>
<br/>
<div style='padding: 10px; border-radius: 5px; border-style: solid; border-color: white'>
 Replace an existing header value by a new value, or append a new header
 to the message.

 # Args

 * `header` - the name of the header to set or add.
 * `value` - the value of the header to set or add.

 # Effective smtp stage

 All of them. Even tought the email is not received at the current stage,
 vsmtp stores new headers and will prepend them to the ones received once
 the `preq` stage is reached.

 Be aware that if you want to set a header value from the original message,
 you must use `set_header` in the `preq` stage and onwards.

 # Example
 ```js
 #{
     postq: [
         action "update subject" || {
             let subject = get_header("Subject");
             set_header("Subject", `${subject} (analysed by vsmtp)`);
         }
     ],
 }
 ```

 

</div>
<br/>
</details>