# Delivery
## Those methods are used to setup the method of delivery for one / every recipient.
<details>
<summary>
<code>
deliver(rcpt)
</code>
</summary>
<br/>
<div style='padding: 10px; border-radius: 5px; border-style: solid; border-color: white'>
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
</details>
<details>
<summary>
<code>
deliver_all()
</code>
</summary>
<br/>
<div style='padding: 10px; border-radius: 5px; border-style: solid; border-color: white'>
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
</details>
<details>
<summary>
<code>
disable_delivery(rcpt)
</code>
</summary>
<br/>
<div style='padding: 10px; border-radius: 5px; border-style: solid; border-color: white'>
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
</details>
<details>
<summary>
<code>
disable_delivery_all()
</code>
</summary>
<br/>
<div style='padding: 10px; border-radius: 5px; border-style: solid; border-color: white'>
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
</details>
<details>
<summary>
<code>
forward(rcpt, target)
</code>
</summary>
<br/>
<div style='padding: 10px; border-radius: 5px; border-style: solid; border-color: white'>
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
</details>
<details>
<summary>
<code>
forward_all(target)
</code>
</summary>
<br/>
<div style='padding: 10px; border-radius: 5px; border-style: solid; border-color: white'>
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
</details>
<details>
<summary>
<code>
maildir(rcpt)
</code>
</summary>
<br/>
<div style='padding: 10px; border-radius: 5px; border-style: solid; border-color: white'>
 Set the delivery method to maildir for a recipient.
 After all rules are evaluated, the email will be stored
 localy in the `~/Maildir/new/` folder of the recipient's user if it exists on the server.

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
</details>
<details>
<summary>
<code>
maildir_all()
</code>
</summary>
<br/>
<div style='padding: 10px; border-radius: 5px; border-style: solid; border-color: white'>
 Set the delivery method to maildir for all recipients.
 After all rules are evaluated, the email will be stored
 localy in each `~/Maildir/new` folder of they respective recipient
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
</details>
<details>
<summary>
<code>
mbox(rcpt)
</code>
</summary>
<br/>
<div style='padding: 10px; border-radius: 5px; border-style: solid; border-color: white'>
 Set the delivery method to mbox for a recipient.
 After all rules are evaluated, the email will be stored
 localy in the mail box of the recipient if it exists on the server.

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
</details>
<details>
<summary>
<code>
mbox_all()
</code>
</summary>
<br/>
<div style='padding: 10px; border-radius: 5px; border-style: solid; border-color: white'>
 Set the delivery method to mbox for all recipients.
 After all rules are evaluated, the email will be stored
 localy in the mail box of all recipients if they exists on the server.

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
</details>