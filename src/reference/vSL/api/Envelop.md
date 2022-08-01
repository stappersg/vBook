# Envelop
<details><summary>add_rcpt_context(rcpt)</summary><br/> Add a new recipient to the envelop. Note that this does not add
 the recipient to the `To` header. Use `add_to_message` for that.

 # Args

 * `rcpt` - the new recipient to add.

 # Effective smtp stage

 All of them.

 # Example
 ```js
 #{
     connect: [
        // always deliver a copy of the message to "john.doe@example.com".
        action "rewrite envelop" || add_rcpt_context("john.doe@example.com"),
     ]
 }
 ```

 # Module:Envelop
</details>
<details><summary>remove_rcpt_context(rcpt)</summary><br/> Remove a recipient from the envelop. Note that this does not remove
 the recipient from the `To` header. Use `remove_to_message` for that.

 # Args

 * `rcpt` - the recipient to remove.

 # Effective smtp stage

 All of them.

 # Example
 ```js
 #{
     preq: [
        // never deliver to "john.doe@example.com".
        action "rewrite envelop" || remove_rcpt_context("john.doe@example.com"),
     ]
 }
 ```

 # Module:Envelop
</details>
<details><summary>rewrite_mail_from(new_addr)</summary><br/> Rewrite the value of the `MAIL FROM` command has well has
 the `From` header.

 # Args

 * `new_addr` - the new sender address to set.

 # Effective smtp stage

 `preq` and onwards.

 # Example
 ```js
 #{
     preq: [
        action "rewrite sender" || rewrite_mail_from("john.doe@example.com"),
     ]
 }
 ```

 # Module:Envelop
</details>
<details><summary>rewrite_mail_from_context(new_addr)</summary><br/> Rewrite the sender received from the `MAIL FROM` command.

 # Args

 * `new_addr` - the new sender address to set.

 # Effective smtp stage

 `mail` and onwards.

 # Example
 ```js
 #{
     preq: [
        action "rewrite envelop" || rewrite_mail_from_context("unknown@example.com"),
     ]
 }
 ```

 # Module:Envelop
</details>
<details><summary>rewrite_rcpt_context(old_addr, new_addr)</summary><br/> Replace a recipient received by a `RCPT TO` command.

 # Args

 * `old_addr` - the recipient to replace.
 * `new_addr` - the new address to use when replacing `old_addr`.

 # Effective smtp stage

 `rcpt` and onwards.

 # Example
 ```js
 #{
     preq: [
        action "rewrite envelop" || rewrite_rcpt_context("john.doe@example.com", "john.main@example.com"),
     ]
 }
 ```

 # Module:Envelop
</details>