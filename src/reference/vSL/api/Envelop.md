# Envelop
The SMTP envelop can be mutated by several function from this module.

<div style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 20px; border-radius: 5px;'>
<h2> fn <em style='color: var(--inline-code-color);'>add_rcpt_envelop</em>(<em style='color: var(--inline-code-color)'>rcpt</em>) </h2>
 Add a new recipient to the envelop. Note that this does not add
 the recipient to the `To` header. Use `add_rcpt_message` for that.

 ### Args

 * `rcpt` - the new recipient to add.

 ### Effective smtp stage

 All of them.

 ### Example
 ```js
 #{
     connect: [
        // always deliver a copy of the message to "john.doe@example.com".
        action "rewrite envelop" || add_rcpt_envelop("john.doe@example.com"),
     ]
 }
 ```

 

</div>
<br/>
<br/>

<div style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 20px; border-radius: 5px;'>
<h2> fn <em style='color: var(--inline-code-color);'>bcc</em>(<em style='color: var(--inline-code-color)'>rcpt</em>) </h2>
 Add a recipient as a blind carbon copy. The equivalent of `add_rcpt_envelop`.

 ### Args

 * `rcpt` - the recipient to add as a blind carbon copy.

 ### Effective smtp stage

 All of them.

 ### Example
 ```js
 #{
     connect: [
        // set "john.doe@example.com" as a blind carbon copy.
        action "bcc" || bcc("john.doe@example.com"),
     ]
 }
 ```

 

</div>
<br/>
<br/>

<div style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 20px; border-radius: 5px;'>
<h2> fn <em style='color: var(--inline-code-color);'>remove_rcpt_envelop</em>(<em style='color: var(--inline-code-color)'>rcpt</em>) </h2>
 Remove a recipient from the envelop. Note that this does not remove
 the recipient from the `To` header. Use `remove_rcpt_message` for that.

 ### Args

 * `rcpt` - the recipient to remove.

 ### Effective smtp stage

 All of them.

 ### Example
 ```js
 #{
     preq: [
        // never deliver to "john.doe@example.com".
        action "rewrite envelop" || remove_rcpt_envelop("john.doe@example.com"),
     ]
 }
 ```

 

</div>
<br/>
<br/>

<div style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 20px; border-radius: 5px;'>
<h2> fn <em style='color: var(--inline-code-color);'>rewrite_mail_from</em>(<em style='color: var(--inline-code-color)'>new_addr</em>) </h2>
 Rewrite the value of the `MAIL FROM` command has well has
 the `From` header.

 ### Args

 * `new_addr` - the new sender address to set.

 ### Effective smtp stage

 `preq` and onwards.

 ### Example
 ```js
 #{
     preq: [
        action "rewrite sender" || rewrite_mail_from("john.doe@example.com"),
     ]
 }
 ```

 

</div>
<br/>
<br/>

<div style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 20px; border-radius: 5px;'>
<h2> fn <em style='color: var(--inline-code-color);'>rewrite_mail_from_envelop</em>(<em style='color: var(--inline-code-color)'>new_addr</em>) </h2>
 Rewrite the sender received from the `MAIL FROM` command.

 ### Args

 * `new_addr` - the new sender address to set.

 ### Effective smtp stage

 `mail` and onwards.

 ### Example
 ```js
 #{
     preq: [
        action "rewrite envelop" || rewrite_mail_from_envelop("unknown@example.com"),
     ]
 }
 ```

 

</div>
<br/>
<br/>

<div style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 20px; border-radius: 5px;'>
<h2> fn <em style='color: var(--inline-code-color);'>rewrite_rcpt_envelop</em>(<em style='color: var(--inline-code-color)'>old_addr</em>, <em style='color: var(--inline-code-color)'>new_addr</em>) </h2>
 Replace a recipient received by a `RCPT TO` command.

 ### Args

 * `old_addr` - the recipient to replace.
 * `new_addr` - the new address to use when replacing `old_addr`.

 ### Effective smtp stage

 `rcpt` and onwards.

 ### Example
 ```js
 #{
     preq: [
        action "rewrite envelop" || rewrite_rcpt_envelop("john.doe@example.com", "john.main@example.com"),
     ]
 }
 ```

 

</div>
<br/>
<br/>