# Connection
## Metadata is available for each client, this module lets you query those metadatas.
<details>
<summary>
<code>
client_address()
</code>
</summary>
<br/>
<div style='padding: 10px; border-radius: 5px; border-style: solid; border-color: white'>
 Get the address of the client.

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

 

</div>
<br/>
</details>
<details>
<summary>
<code>
client_ip()
</code>
</summary>
<br/>
<div style='padding: 10px; border-radius: 5px; border-style: solid; border-color: white'>
 Get the ip address of the client.

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

 

</div>
<br/>
</details>
<details>
<summary>
<code>
client_port()
</code>
</summary>
<br/>
<div style='padding: 10px; border-radius: 5px; border-style: solid; border-color: white'>
 Get the ip port of the client.

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

 

</div>
<br/>
</details>
<details>
<summary>
<code>
connection_timestamp()
</code>
</summary>
<br/>
<div style='padding: 10px; border-radius: 5px; border-style: solid; border-color: white'>
 Get a the timestamp of the client's connection time.

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

 

</div>
<br/>
</details>
<details>
<summary>
<code>
server_address()
</code>
</summary>
<br/>
<div style='padding: 10px; border-radius: 5px; border-style: solid; border-color: white'>
 Get the full server address.

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

 

</div>
<br/>
</details>
<details>
<summary>
<code>
server_ip()
</code>
</summary>
<br/>
<div style='padding: 10px; border-radius: 5px; border-style: solid; border-color: white'>
 Get the server's ip.

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

 

</div>
<br/>
</details>
<details>
<summary>
<code>
server_name()
</code>
</summary>
<br/>
<div style='padding: 10px; border-radius: 5px; border-style: solid; border-color: white'>
 Get the name of the server.

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

 

</div>
<br/>
</details>
<details>
<summary>
<code>
server_port()
</code>
</summary>
<br/>
<div style='padding: 10px; border-radius: 5px; border-style: solid; border-color: white'>
 Get the server's port.

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

 

</div>
<br/>
</details>