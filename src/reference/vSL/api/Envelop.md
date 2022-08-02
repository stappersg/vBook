# Envelop
## The SMTP envelop can be mutated by several function from this module.
<details><summary>add_rcpt_envelop(rcpt)</summary><br/> Add a new recipient to the envelop. Note that this does not add
 the recipient to the `To` header. Use `add_rcpt_message` for that.

 # Args

 * `rcpt` - the new recipient to add.

 # Effective smtp stage

 All of them.

 # Example
 ```js
 #{
     connect: [
        // always deliver a copy of the message to "john.doe@example.com".
        action "rewrite envelop" || add_rcpt_envelop("john.doe@example.com"),
     ]
 }
 ```

 
</details>
<details><summary>remove_rcpt_envelop(rcpt)</summary><br/> Remove a recipient from the envelop. Note that this does not remove
 the recipient from the `To` header. Use `remove_rcpt_message` for that.

 # Args

 * `rcpt` - the recipient to remove.

 # Effective smtp stage

 All of them.

 # Example
 ```js
 #{
     preq: [
        // never deliver to "john.doe@example.com".
        action "rewrite envelop" || remove_rcpt_envelop("john.doe@example.com"),
     ]
 }
 ```

 
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

 
</details>
<details><summary>rewrite_mail_from_envelop(new_addr)</summary><br/> Rewrite the sender received from the `MAIL FROM` command.

 # Args

 * `new_addr` - the new sender address to set.

 # Effective smtp stage

 `mail` and onwards.

 # Example
 ```js
 #{
     preq: [
        action "rewrite envelop" || rewrite_mail_from_envelop("unknown@example.com"),
     ]
 }
 ```

 
</details>
<details><summary>rewrite_rcpt_envelop(old_addr, new_addr)</summary><br/> Replace a recipient received by a `RCPT TO` command.

 # Args

 * `old_addr` - the recipient to replace.
 * `new_addr` - the new address to use when replacing `old_addr`.

 # Effective smtp stage

 `rcpt` and onwards.

 # Example
 ```js
 #{
     preq: [
        action "rewrite envelop" || rewrite_rcpt_envelop("john.doe@example.com", "john.main@example.com"),
     ]
 }
 ```

 
</details>