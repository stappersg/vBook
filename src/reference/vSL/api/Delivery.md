# Delivery
## Those methods are used to setup the method of delivery for one / every recipient.

<div style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 20px; border-radius: 5px;'>
<h1> fn <em style='color: var(--inline-code-color);'>deliver</em>(<em style='color: var(--inline-code-color)'>rcpt</em>) </h1>
 Set the delivery method to deliver for a single recipient.
 After all rules are evaluated, the email will be sent
 to the recipient using the domain of its address.

 # Args

 * `rcpt` - the recipient to apply the method to.

 # Effective smtp stage

 All of them.

 # Example
 ```js
 #{
     delivery: [
        action "setup delivery" || deliver("john.doe@example.com"),
     ]
 }
 ```

 

</div>
<br/>
<br/>

<div style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 20px; border-radius: 5px;'>
<h1> fn <em style='color: var(--inline-code-color);'>deliver_all</em>() </h1>
 Set the delivery method to deliver for all recipients.
 After all rules are evaluated, the email will be sent
 to all recipients using the domain of their respective address.

 # Effective smtp stage

 All of them.

 # Example
 ```js
 #{
     delivery: [
        action "setup delivery" || deliver_all(),
     ]
 }
 ```

 

</div>
<br/>
<br/>

<div style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 20px; border-radius: 5px;'>
<h1> fn <em style='color: var(--inline-code-color);'>disable_delivery</em>(<em style='color: var(--inline-code-color)'>rcpt</em>) </h1>
 Disable the delivery for a single recipient.

 # Args

 * `rcpt` - the recipient to apply the method to.

 # Effective smtp stage

 All of them.

 # Example
 ```js
 #{
     delivery: [
        action "disable delivery" || disable_delivery("john.doe@example.com"),
     ]
 }
 ```

 

</div>
<br/>
<br/>

<div style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 20px; border-radius: 5px;'>
<h1> fn <em style='color: var(--inline-code-color);'>disable_delivery_all</em>() </h1>
 Disable delivery for all single recipients.

 # Effective smtp stage

 All of them.

 # Example
 ```js
 #{
     delivery: [
        action "disable delivery" || disable_delivery_all(),
     ]
 }
 ```

 

</div>
<br/>
<br/>

<div style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 20px; border-radius: 5px;'>
<h1> fn <em style='color: var(--inline-code-color);'>forward</em>(<em style='color: var(--inline-code-color)'>rcpt</em>, <em style='color: var(--inline-code-color)'>target</em>) </h1>
 Set the delivery method to forwarding for a single recipient.
 After all rules are evaluated, forwarding will be used to deliver
 the email to the recipient.

 # Args

 * `rcpt` - the recipient to apply the method to.
 * `target` - the target to forward the email to.

 # Effective smtp stage

 All of them.

 # Example
 ```js
 #{
     delivery: [
        action "setup forwarding" || forward("john.doe@example.com", "mta-john.example.com"),
     ]
 }
 ```

 

</div>
<br/>
<br/>

<div style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 20px; border-radius: 5px;'>
<h1> fn <em style='color: var(--inline-code-color);'>forward_all</em>(<em style='color: var(--inline-code-color)'>target</em>) </h1>
 Set the delivery method to forwarding for all recipients.
 After all rules are evaluated, forwarding will be used to deliver
 the email.

 # Args

 * `target` - the target to forward the email to.

 # Effective smtp stage

 All of them.

 # Example
 ```js
 #{
     delivery: [
        action "setup forwarding" || forward_all("mta-john.example.com"),
     ]
 }
 ```

 

</div>
<br/>
<br/>

<div style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 20px; border-radius: 5px;'>
<h1> fn <em style='color: var(--inline-code-color);'>maildir</em>(<em style='color: var(--inline-code-color)'>rcpt</em>) </h1>
 Set the delivery method to maildir for a recipient.
 After all rules are evaluated, the email will be stored
 locally in the `~/Maildir/new/` folder of the recipient's user if it exists on the server.

 # Args

 * `rcpt` - the recipient to apply the method to.

 # Effective smtp stage

 All of them.

 # Example
 ```js
 #{
     delivery: [
        action "setup maildir" || maildir("john.doe@example.com"),
     ]
 }
 ```

 

</div>
<br/>
<br/>

<div style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 20px; border-radius: 5px;'>
<h1> fn <em style='color: var(--inline-code-color);'>maildir_all</em>() </h1>
 Set the delivery method to maildir for all recipients.
 After all rules are evaluated, the email will be stored
 locally in each `~/Maildir/new` folder of they respective recipient
 if they exists on the server.

 # Effective smtp stage

 All of them.

 # Example
 ```js
 #{
     delivery: [
        action "setup mbox" || mbox_all(),
     ]
 }
 ```

 

</div>
<br/>
<br/>

<div style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 20px; border-radius: 5px;'>
<h1> fn <em style='color: var(--inline-code-color);'>mbox</em>(<em style='color: var(--inline-code-color)'>rcpt</em>) </h1>
 Set the delivery method to mbox for a recipient.
 After all rules are evaluated, the email will be stored
 locally in the mail box of the recipient if it exists on the server.

 # Args

 * `rcpt` - the recipient to apply the method to.

 # Effective smtp stage

 All of them.

 # Example
 ```js
 #{
     delivery: [
        action "setup mbox" || mbox("john.doe@example.com"),
     ]
 }
 ```

 

</div>
<br/>
<br/>

<div style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 20px; border-radius: 5px;'>
<h1> fn <em style='color: var(--inline-code-color);'>mbox_all</em>() </h1>
 Set the delivery method to mbox for all recipients.
 After all rules are evaluated, the email will be stored
 locally in the mail box of all recipients if they exists on the server.

 # Effective smtp stage

 All of them.

 # Example
 ```js
 #{
     delivery: [
        action "setup mbox" || mbox_all(),
     ]
 }
 ```

 

</div>
<br/>
<br/>