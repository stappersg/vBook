# Delivery
<details><summary>deliver(rcpt)</summary><br/> Set the delivery method to deliver for a single recipient.
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

 # Module:Delivery
</details>
<details><summary>deliver_all()</summary><br/> Set the delivery method to deliver for all recipients.
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

 # Module:Delivery
</details>
<details><summary>disable_delivery(rcpt)</summary><br/> Disable the delivery for a single recipient.

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

 # Module:Delivery
</details>
<details><summary>disable_delivery_all()</summary><br/> Disable delivery for all single recipients.

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

 # Module:Delivery
</details>
<details><summary>forward(rcpt, target)</summary><br/> Set the delivery method to forwarding for a single recipient.
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

 # Module:Delivery
</details>
<details><summary>forward_all(target)</summary><br/> Set the delivery method to forwarding for all recipients.
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

 # Module:Delivery
</details>
<details><summary>maildir(rcpt)</summary><br/> Set the delivery method to maildir for a recipient.
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

 # Module:Delivery
</details>
<details><summary>maildir_all()</summary><br/> Set the delivery method to maildir for all recipients.
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

 # Module:Delivery
</details>
<details><summary>mbox(rcpt)</summary><br/> Set the delivery method to mbox for a recipient.
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

 # Module:Delivery
</details>
<details><summary>mbox_all()</summary><br/> Set the delivery method to mbox for all recipients.
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

 # Module:Delivery
</details>