# Transaction
## At each SMTP stage, data from the client is received via 'SMTP commands'. This module lets you query the content of the commands.
<details>
<summary>
<code>
helo()
</code>
</summary>
<br/>
<div style='padding: 10px; border-radius: 5px; border-style: solid; border-color: white'>
 Get the value of the `HELO/EHLO` command sent by the client.

 # Effective smtp stage

 `helo` and onwards.

 # Return

 * `string` - the value of the `HELO/EHLO` command.

 # Example
 ```js
 #{
     helo: [
        action "log info" || log("info", `${helo()}`),
     ]
 }
 ```

 

</div>
<br/>
</details>
<details>
<summary>
<code>
mail_from()
</code>
</summary>
<br/>
<div style='padding: 10px; border-radius: 5px; border-style: solid; border-color: white'>
 Get the value of the `MAIL FROM` command sent by the client.

 # Effective smtp stage

 `mail` and onwards.

 # Return

 * `address` - the sender address.

 # Example
 ```js
 #{
     helo: [
        action "log info" || log("info", `${mail_from()}`),
     ]
 }
 ```

 

</div>
<br/>
</details>
<details>
<summary>
<code>
mail_timestamp()
</code>
</summary>
<br/>
<div style='padding: 10px; border-radius: 5px; border-style: solid; border-color: white'>
 Get the time of reception of the email.

 # Effective smtp stage

 `preq` and onwards.

 # Return

 * `string` - the timestamp.

 # Example
 ```js
 #{
     preq: [
        action "receiving the email" || log("info", `time of reception: ${mail_timestamp()}`),
     ]
 }
 ```

 

</div>
<br/>
</details>
<details>
<summary>
<code>
message_id()
</code>
</summary>
<br/>
<div style='padding: 10px; border-radius: 5px; border-style: solid; border-color: white'>
 Get the unique id of the received message.

 # Effective smtp stage

 `preq` and onwards.

 # Return

 * `string` - the message id.

 # Example
 ```js
 #{
     preq: [
        action "message received" || log("info", `message id: ${message_id()}`),
     ]
 }
 ```

 

</div>
<br/>
</details>
<details>
<summary>
<code>
rcpt()
</code>
</summary>
<br/>
<div style='padding: 10px; border-radius: 5px; border-style: solid; border-color: white'>
 Get the value of the current `RCPT TO` command sent by the client.

 # Effective smtp stage

 `rcpt` and onwards. Please note that `rcpt()` will always return
 the last recipient received in stages after the `rcpt` stage. Therefore,
 this functions is best used in the `rcpt` stage.

 # Return

 * `address` - the address of the received recipient.

 # Example
 ```js
 #{
     rcpt: [
        action "log recipients" || log("info", `new recipient: ${rcpt()}`),
     ]
 }
 ```

 

</div>
<br/>
</details>
<details>
<summary>
<code>
rcpt_list()
</code>
</summary>
<br/>
<div style='padding: 10px; border-radius: 5px; border-style: solid; border-color: white'>
 Get the list of recipients received by the client.

 # Effective smtp stage

 `rcpt` and onwards. Note that you will not have all recipients received
 all at once in the `rcpt` stage. It is better to use this function
 in the later stages.

 # Return

 * `Array of addresses` - the list containing all recipients.

 # Example
 ```js
 #{
     preq: [
        action "log recipients" || log("info", `all recipients: ${rcpt_list()}`),
     ]
 }
 ```

 

</div>
<br/>
</details>