# Utils
## Those miscellaneous functions lets you query data from your system, log stuff, perform dns lookups etc ...
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

 
</details>
<details><summary>lookup(host)</summary><br/> Performs a dual-stack DNS lookup for the given hostname.

 # Args

 * `host` - A valid hostname to search.

 # Return

 * `array` - an array of IPs. The array is empty if no IPs were found for the host.

 # Effective smtp stage

 All of them.

 # Example
 ```js
 #{
     rcpt: [
        action "perform lookup" || {
             let domain = rcpt().domain;
             let ips = lookup(domain);

             print(`ips found for ${domain}`);
             for ip in ips {
                 print(`- ${ip}`);
             }
        }
     ]
 }
 ```

 
</details>
<details><summary>rlookup(ip)</summary><br/> Performs a reverse lookup for the given IP.

 # Args

 * `ip` - The IP to query.

 # Return

 * `array` - an array of FQDNs. The array is empty if nothing was found.

 # Effective smtp stage

 All of them.

 # Example
 ```js
 #{
     connect: [
        action "perform reverse lookup" || {
             let domains = rlookup(client_ip());

             print(`domains found for ip ${client_ip()}`);
             for domain in domains {
                 print(`- ${domain}`);
             }
        }
     ]
 }
 ```

 
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

 
</details>