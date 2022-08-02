# Services
## Services are external programs that can be used via the functions available in this module.
<details><summary>get(key)</summary><br/> Get the value of a key in a database.

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

 
</details>
<details><summary>rm(key)</summary><br/> Remove a record from a database.

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

 
</details>
<details><summary>set(record)</summary><br/> Set a record into a database.

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

 
</details>