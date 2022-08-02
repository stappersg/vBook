# Transaction
## At each SMTP stage, data from the client is received via 'SMTP commands'. This module lets you query the content of the commands.
<details><summary>helo()</summary><br/> Get the value of the `HELO/EHLO` command sent by the client.

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

 
</details>
<details><summary>mail_from()</summary><br/> Get the value of the `MAIL FROM` command sent by the client.

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

 
</details>
<details><summary>mail_timestamp()</summary><br/> Get the time of reception of the email.

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

 
</details>
<details><summary>message_id()</summary><br/> Get the unique id of the received message.

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

 
</details>
<details><summary>rcpt()</summary><br/> Get the value of the current `RCPT TO` command sent by the client.

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

 
</details>
<details><summary>rcpt_list()</summary><br/> Get the list of recipients received by the client.

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

 
</details>