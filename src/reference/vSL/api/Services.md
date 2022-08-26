# Services
## Services are external programs that can be used via the functions available in this module.
<details>
<summary>
<code>
get(key)
</code>
</summary>
<br/>
<div style='padding: 10px; border-radius: 5px; border-style: solid; border-color: white'>
 Get the value of a key in a database.

 # Args

 * `key` - the key to query.

 # Return

 * `Array of records` - an array containing the results.

 # Effective smtp stage

 All of them.

 # Example
 ```js
 import "services" as svc;

 #{
     mail: [
        action "fetch database" || {
             let records = svc::my_database.get(mail_from());

             if records.len() == 0 {
                 log("debug", `${mail_from()} is not in my database`);
             } else {
                 log("debug", `${mail_from()} found in my database`);
             }
        }
     ]
 }
 ```

 

</div>
<br/>
</details>
<details>
<summary>
<code>
rm(key)
</code>
</summary>
<br/>
<div style='padding: 10px; border-radius: 5px; border-style: solid; border-color: white'>
 Remove a record from a database.

 # Args

 * `key` - the key to remove.

 # Effective smtp stage

 All of them.

 # Example
 ```js
 import "services" as svc;

 #{
     mail: [
        action "remove sender from database" || {
             svc::my_database.rm(mail_from());
        }
     ]
 }
 ```

 

</div>
<br/>
</details>
<details>
<summary>
<code>
run()
</code>
</summary>
<br/>
<div style='padding: 10px; border-radius: 5px; border-style: solid; border-color: white'>
 Run a command from a `cmd` service.

 # Effective smtp stage

 All of them.

 # Example

 ```js
 // services.vsl
 service echo cmd = #{
     timeout: "2s",
     command: "echo",
     args: ["-e", "using cmd to print to stdout\r\n"],
 };
 ```

 ```js
 // main.vsl
 import "services" as svc;

 #{
     connect: [
        action "execute command" || {
             // prints 'using cmd to print to stdout\r\n' on the screen.
             svc::echo.cmd_run();
        }
     ]
 }
 ```

 

</div>
<br/>
</details>
<details>
<summary>
<code>
run(args)
</code>
</summary>
<br/>
<div style='padding: 10px; border-radius: 5px; border-style: solid; border-color: white'>
 Run a command from a `cmd` service with arguments.
 This allows you to run a command with dynamic arguments.

 # Args

 * `args` - an array of strings that will replace current command
            arguments defined in the `args` field of a `cmd` service.

 # Effective smtp stage

 All of them.

 # Example

 ```js
 // services.vsl
 service echo cmd = #{
     timeout: "2s",
     command: "echo",
     args: ["-e", "using cmd to print to stdout\r\n"],
 };
 ```

 ```js
 // main.vsl
 import "services" as svc;

 #{
     rcpt: [
        action "print recipient using command" || {
             // prints all recipients using the `echo` command.
             svc::echo.cmd_run(["-E", "-n", `new recipient: ${rcpt()}`]);
        }
     ]
 }
 ```

 

</div>
<br/>
</details>
<details>
<summary>
<code>
set(record)
</code>
</summary>
<br/>
<div style='padding: 10px; border-radius: 5px; border-style: solid; border-color: white'>
 Set a record into a database.

 # Args

 * `record` - the record to set.

 # Effective smtp stage

 All of them.

 # Example
 ```js
 import "services" as svc;

 #{
     mail: [
        action "set sender in database" || {
             svc::my_database.set(mail_from());
        }
     ]
 }
 ```

 

</div>
<br/>
</details>