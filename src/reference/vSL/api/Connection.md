# Connection
## Metadata is available for each client, this module lets you query those metadatas.
<details><summary>client_address()</summary><br/> Get the address of the client.

 # Effective smtp stage

 All of them.

 # Return

 * `string` - the client's address with the `ip:port` format.

 # Example
 ```js
 #{
     connect: [
        action "log info" || log("info", `${client_address()}`),
     ]
 }
 ```

 
</details>
<details><summary>client_ip()</summary><br/> Get the ip address of the client.

 # Effective smtp stage

 All of them.

 # Return

 * `string` - the client's ip address.

 # Example
 ```js
 #{
     connect: [
        action "log info" || log("info", `${client_ip()}`),
     ]
 }
 ```

 
</details>
<details><summary>client_port()</summary><br/> Get the ip port of the client.

 # Effective smtp stage

 All of them.

 # Return

 * `int` - the client's port.

 # Example
 ```js
 #{
     connect: [
        action "log info" || log("info", `${client_port()}`),
     ]
 }
 ```

 
</details>
<details><summary>connection_timestamp()</summary><br/> Get a the timestamp of the client's connection time.

 # Effective smtp stage

 All of them.

 # Return

 * `timestamp` - the connexion timestamp of the client.

 # Example
 ```js
 #{
     connect: [
        action "log info" || log("info", `${connection_timestamp()}`),
     ]
 }
 ```

 
</details>
<details><summary>server_address()</summary><br/> Get the full server address.

 # Effective smtp stage

 All of them.

 # Return

 * `string` - the server's address with the `ip:port` format.

 # Example
 ```js
 #{
     connect: [
        action "log info" || log("info", `${server_address()}`),
     ]
 }
 ```

 
</details>
<details><summary>server_ip()</summary><br/> Get the server's ip.

 # Effective smtp stage

 All of them.

 # Return

 * `string` - the server's ip.

 # Example
 ```js
 #{
     connect: [
        action "log info" || log("info", `${server_ip()}`),
     ]
 }
 ```

 
</details>
<details><summary>server_name()</summary><br/> Get the name of the server.

 # Effective smtp stage

 All of them.

 # Return

 * `string` - the name of the server.

 # Example
 ```js
 #{
     connect: [
        action "log info" || log("info", `${server_name()}`),
     ]
 }
 ```

 
</details>
<details><summary>server_port()</summary><br/> Get the server's port.

 # Effective smtp stage

 All of them.

 # Return

 * `string` - the server's port.

 # Example
 ```js
 #{
     connect: [
        action "log info" || log("info", `${server_port()}`),
     ]
 }
 ```

 
</details>