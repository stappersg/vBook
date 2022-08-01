# Message
<details><summary>add_to_message(addr)</summary><br/> Add a recipient to the `To` header of the message.

 # Args

 * `addr` - the recipient address to add to the `To` header.

 # Effective smtp stage

 `preq` and onwards.

 # Example
 ```js
 #{
     preq: [
        action "update recipients" || add_to_message("john.doe@example.com"),
     ]
 }
 ```

 # Module:Message
</details>
<details><summary>append_header(header, value)</summary><br/> Append a new header to the message.

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

 # Module:Message
</details>
<details><summary>bcc(rcpt)</summary><br/> Add a recipient as a blind carbon copy. The equivalent of `add_rcpt`.

 # Args

 * `rcpt` - the recipient to add as a blind carbon copy.

 # Effective smtp stage

 All of them.

 # Example
 ```js
 #{
     connect: [
        // set "john.doe@example.com" as a blind carbon copy.
        action "bcc" || bcc("john.doe@example.com"),
     ]
 }
 ```

 # Module:Message
</details>
<details><summary>get_header(header)</summary><br/> Get a specific header from the incoming message.

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

 # Module:Message
</details>
<details><summary>has_header(header)</summary><br/> Checks if the message contains a specific header.

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

 # Module:Message
</details>
<details><summary>prepend_header(header, value)</summary><br/> Prepend a new header to the message.

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

 # Module:Message
</details>
<details><summary>remove_to_message(addr)</summary><br/> Remove a recipient from the `To` header of the message.

 # Args

 * `addr` - the recipient to remove to the `To` header.

 # Effective smtp stage

 `preq` and onwards.

 # Example
 ```js
 #{
     preq: [
        action "update recipients" || remove_to_message("john.doe@example.com"),
     ]
 }
 ```

 # Module:Message
</details>
<details><summary>rewrite_mail_from_message(new_addr)</summary><br/> Change the sender's address in the `From` header of the message.

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

 # Module:Message
</details>
<details><summary>rewrite_to_message(old_addr, new_addr)</summary><br/> Replace a recipient by an other in the `To` header of the message.

 # Args

 * `old_addr` - the recipient to replace.
 * `new_addr` - the new address to use when replacing `old_addr`.

 # Effective smtp stage

 `preq` and onwards.

 # Example
 ```js
 #{
     preq: [
        action "rewrite recipient" || rewrite_to_message("john.doe@example.com", "john-mta@example.com"),
     ]
 }
 ```

 # Module:Message
</details>
<details><summary>set_header(header, value)</summary><br/> Replace an existing header value by a new value, or append a new header
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

 # Module:Message
</details>