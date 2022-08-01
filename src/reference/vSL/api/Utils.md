# Utils
<details><summary>date()</summary><br/> Get the current date.

 # Return

 * `string` - the current date.

 # Effective smtp stage

 All of them.

 # Example
 ```js
 #{
     preq: [
        action "append info header" || {
             append_header("X-VSMTP", `email received by ${hostname()} the ${date()}.`);
        }
     ]
 }
 ```

 # Module:Utils
</details>
<details><summary>dump(dir)</summary><br/> Export the current message and the envelop to a file as a `json` file.
 The message id of the email is used to name the file.

 # Args

 * `dir` - the directory where to store the data. Relative to the
 application path.

 # Effective smtp stage

 `preq` and onwards.

 # Example
 ```js
 #{
     preq: [
        action "dump email" || dump("metadatas"),
     ]
 }
 ```

 # Module:Utils
</details>
<details><summary>hostname()</summary><br/> Get the hostname of this machine.

 # Return

 * `string` - the host name of the machine.

 # Effective smtp stage

 All of them.

 # Example
 ```js
 #{
     preq: [
        action "append info header" || {
             append_header("X-VSMTP", `email received by ${hostname()}.`);
        }
     ]
 }
 ```

 # Module:Utils
</details>
<details><summary>in_domain(rcpt)</summary><br/> check if the recipient passed as argument is part of the
 domains (root & sni) of the server.

 # Args

 * `rcpt` - the recipient to check, of type string | `object address` | rcpt.

 # Return

 * `bool` - true of the recipient's domain is part of the server's root or sni domains, false otherwise.

 # Effective smtp stage
 all of them, but should be use in the rcpt stage.

 # Example
 ```js
 #{
     rcpt: [
        rule "check rcpt domain" || if in_domain(ctx().rcpt) { next() } else { deny() },
     ]
 }

 # Module:Utils
 ```
</details>
<details><summary>log(level, message)</summary><br/> Log information to stdout in `nodaemon` mode or to a file.

 # Args

 * `level` - the level of the message, can be "trace", "debug", "info", "warn" or "error".
 * `message` - the message to log.

 # Effective smtp stage

 All of them.

 # Example
 ```js
 #{
     preq: [
        action "log info" || log("info", "this is an informational log."),
     ]
 }
 ```

 # Module:Utils
</details>
<details><summary>time()</summary><br/> Get the current time.

 # Return

 * `string` - the current time.

 # Effective smtp stage

 All of them.

 # Example
 ```js
 #{
     preq: [
        action "append info header" || {
             append_header("X-VSMTP", `email received by ${hostname()} the ${date()} at ${time()}.`);
        }
     ]
 }
 ```

 # Module:Utils
</details>
<details><summary>user_exist(name)</summary><br/> Check if a user exists on this server.

 # Args

 * `name` - the name of the user.

 # Return

 * `bool` - true if the user exists, false otherwise.

 # Effective smtp stage

 All of them.

 # Example
 ```js
 #{
     rcpt: [
        action "check for local user" || {
            if user_exist(rcpt().local_part) {
                log("debug", `${rcpt().local_part} exists on disk.`);
            }
        }
     ]
 }
 ```

 # Module:Utils
</details>
<details><summary>write(dir)</summary><br/> Export the current raw message to a file as an `eml` file.
 The message id of the email is used to name the file.

 # Args

 * `dir` - the directory where to store the email. Relative to the
 application path.

 # Effective smtp stage

 `preq` and onwards.

 # Example
 ```js
 #{
     preq: [
        action "write to file" || write("archives"),
     ]
 }
 ```

 # Module:Utils
</details>