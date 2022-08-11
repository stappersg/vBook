# Utils
## Those miscellaneous functions lets you query data from your system, log stuff, perform dns lookups etc ...
<details>
<summary>
<code>
date()
</code>
</summary>
<br/>
<div style='padding: 10px; border-radius: 5px; border-style: solid; border-color: white'>
 Get the current date.

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

 

</div>
<br/>
</details>
<details>
<summary>
<code>
dump(dir)
</code>
</summary>
<br/>
<div style='padding: 10px; border-radius: 5px; border-style: solid; border-color: white'>
 Export the current message and the envelop to a file as a `json` file.
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

 

</div>
<br/>
</details>
<details>
<summary>
<code>
hostname()
</code>
</summary>
<br/>
<div style='padding: 10px; border-radius: 5px; border-style: solid; border-color: white'>
 Get the hostname of this machine.

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

 

</div>
<br/>
</details>
<details>
<summary>
<code>
in_domain(rcpt)
</code>
</summary>
<br/>
<div style='padding: 10px; border-radius: 5px; border-style: solid; border-color: white'>
 check if the recipient passed as argument is part of the
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

</div>
<br/>
</details>
<details>
<summary>
<code>
log(level, message)
</code>
</summary>
<br/>
<div style='padding: 10px; border-radius: 5px; border-style: solid; border-color: white'>
 Log information to stdout in `nodaemon` mode or to a file.

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

 

</div>
<br/>
</details>
<details>
<summary>
<code>
lookup(host)
</code>
</summary>
<br/>
<div style='padding: 10px; border-radius: 5px; border-style: solid; border-color: white'>
 Performs a dual-stack DNS lookup for the given hostname.

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

 

</div>
<br/>
</details>
<details>
<summary>
<code>
rlookup(ip)
</code>
</summary>
<br/>
<div style='padding: 10px; border-radius: 5px; border-style: solid; border-color: white'>
 Performs a reverse lookup for the given IP.

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

 

</div>
<br/>
</details>
<details>
<summary>
<code>
time()
</code>
</summary>
<br/>
<div style='padding: 10px; border-radius: 5px; border-style: solid; border-color: white'>
 Get the current time.

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

 

</div>
<br/>
</details>
<details>
<summary>
<code>
user_exist(name)
</code>
</summary>
<br/>
<div style='padding: 10px; border-radius: 5px; border-style: solid; border-color: white'>
 Check if a user exists on this server.

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

 

</div>
<br/>
</details>
<details>
<summary>
<code>
write(dir)
</code>
</summary>
<br/>
<div style='padding: 10px; border-radius: 5px; border-style: solid; border-color: white'>
 Export the current raw message to a file as an `eml` file.
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

 

</div>
<br/>
</details>