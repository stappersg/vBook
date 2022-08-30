# Connection
## Metadata is available for each client, this module lets you query those metadatas.

<div style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 20px; border-radius: 5px;'>
<h1> fn <em style='color: var(--inline-code-color);'>client_address</em>() </h1>
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
<br/>

<div style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 20px; border-radius: 5px;'>
<h1> fn <em style='color: var(--inline-code-color);'>client_ip</em>() </h1>
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
<br/>

<div style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 20px; border-radius: 5px;'>
<h1> fn <em style='color: var(--inline-code-color);'>client_port</em>() </h1>
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
<br/>

<div style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 20px; border-radius: 5px;'>
<h1> fn <em style='color: var(--inline-code-color);'>connection_timestamp</em>() </h1>
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
<br/>

<div style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 20px; border-radius: 5px;'>
<h1> fn <em style='color: var(--inline-code-color);'>server_address</em>() </h1>
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
<br/>

<div style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 20px; border-radius: 5px;'>
<h1> fn <em style='color: var(--inline-code-color);'>server_ip</em>() </h1>
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
<br/>

<div style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 20px; border-radius: 5px;'>
<h1> fn <em style='color: var(--inline-code-color);'>server_name</em>() </h1>
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
<br/>

<div style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 20px; border-radius: 5px;'>
<h1> fn <em style='color: var(--inline-code-color);'>server_port</em>() </h1>
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
<br/>