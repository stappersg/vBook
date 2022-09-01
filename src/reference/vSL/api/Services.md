# Services
Services are external programs that can be used via the functions available in this module.

<div style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 20px; border-radius: 5px;'>
<h2> fn <em style='color: var(--inline-code-color);'>get</em>(<em style='color: var(--inline-code-color)'>key</em>) </h2>
 Get the value of a key in a csv database.

 ### Args

 * `key` - the key to query.

 ### Return

 * `Array of records` - an array containing the results. If no record is found,
                        an empty array is returned.

 ### Effective smtp stage

 All of them.

 ### Example
 ```js
 import "services" as svc;

 #{
     mail: [
        action "fetch database" || {
             let records = svc::my_database.get(mail_from());

             if records == [] {
                 log("debug", `${mail_from()} is not in my database`);
             } else {
                 log("debug", `${mail_from()} found in my database: ${records}`);
             }
        }
     ]
 }
 ```

 

</div>
<br/>
<br/>

<div style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 20px; border-radius: 5px;'>
<h2> fn <em style='color: var(--inline-code-color);'>query</em>(<em style='color: var(--inline-code-color)'>q</em>) </h2>
 Query a database.

 ### Args

 * `q` - the query to execute.

 ### Effective smtp stage

 All of them.

 ### Example

 ```js
 service my_db db:mysql = #{
     url: "mysql://localhost/",
     user: "guest",
 };
 ```

 ```js
 import "services" as svc;

 #{
     connect: [
        action "log database" || {
             let version_record = svc::my_db.query("SELECT version();");
             // Result is a array of maps: [ #{"version()": "'version-of-mysql'"} ]
             log("trace", `Database version is ${version_record[0]["version()"]}`);

             // Fetching a 'greylist' database with a 'sender' table containing the (user, domain, address) fields.
             let senders = svc::my_db.query("SELECT * FROM greylist.sender");

             // Iterate over rows.
             for sender in senders {
                 // You can access the columns values using Rhai's Map syntax:
                 print(`name: ${sender.user}, domain: ${sender.domain}, address: ${sender.address}`);
             }

             // Populate the database with a new record.
             svc::my_db.query(`INSERT INTO greylist.sender (user, domain, address) values ("john.doe", "example.com", "john.doe@example.com");`);
        }
     ]
 }
 ```

 

</div>
<br/>
<br/>

<div style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 20px; border-radius: 5px;'>
<h2> fn <em style='color: var(--inline-code-color);'>rm</em>(<em style='color: var(--inline-code-color)'>key</em>) </h2>
 Remove a record from a csv database.

 ### Args

 * `key` - the key to remove.

 ### Effective smtp stage

 All of them.

 ### Example
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
<br/>

<div style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 20px; border-radius: 5px;'>
<h2> fn <em style='color: var(--inline-code-color);'>run</em>(<em style='color: var(--inline-code-color)'>args</em>) </h2>
 Run a command from a `cmd` service with arguments.
 This allows you to run a command with dynamic arguments.

 ### Args

 * `args` - an array of strings that will replace current command
            arguments defined in the `args` field of a `cmd` service.

 ### Effective smtp stage

 All of them.

 ### Example

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
<br/>

<div style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 20px; border-radius: 5px;'>
<h2> fn <em style='color: var(--inline-code-color);'>set</em>(<em style='color: var(--inline-code-color)'>record</em>) </h2>
 Set a record into a csv database.

 ### Args

 * `record` - the record to set.

 ### Effective smtp stage

 All of them.

 ### Example
 ```js
 import "services" as svc;

 #{
     mail: [
        action "set sender in database" || {
             svc::my_database.set([ mail_from() ]);
        }
     ]
 }
 ```

 

</div>
<br/>
<br/>