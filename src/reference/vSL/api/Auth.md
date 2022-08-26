# Auth
## This module contains authentication mechanisms to secure your server.
<details>
<summary>
<code>
auth()
</code>
</summary>
<br/>
<div style='padding: 10px; border-radius: 5px; border-style: solid; border-color: white'>
 Get authentication credentials from the client.

 # Effective smtp stage

 `authenticate` only.

 # Return

 * `Credentials` - the credentials of the client.

 # Example
 ```js
 #{
     authenticate: [
        action "log info" || log("info", `${auth()}`),
     ]
 }
 ```

 

</div>
<br/>
</details>
<details>
<summary>
<code>
authenticate()
</code>
</summary>
<br/>
<div style='padding: 10px; border-radius: 5px; border-style: solid; border-color: white'>
 Process the SASL authentication mechanism.

 The current implementation support "PLAIN" mechanism, and will call the
 `testsaslauthd` program to check the credentials.

 The credentials will be verified depending on the mode of `saslauthd`.

 A native implementation will be provided in the future.

 

</div>
<br/>
</details>
<details>
<summary>
<code>
is_authenticated()
</code>
</summary>
<br/>
<div style='padding: 10px; border-radius: 5px; border-style: solid; border-color: white'>
 Check if the client is authenticated.

 # Effective smtp stage

 `authenticate` only.

 # Return

 * `bool` - true if the client succeeded to authenticate itself, false otherwise.

 # Example
 ```js
 #{
     authenticate: [
        action "log info" || log("info", `${is_authenticated()}`),
     ]
 }
 ```

 

</div>
<br/>
</details>
<details>
<summary>
<code>
is_secured()
</code>
</summary>
<br/>
<div style='padding: 10px; border-radius: 5px; border-style: solid; border-color: white'>
 Check if the client's connexion was secure.

 # Effective smtp stage

 `authenticate` only.

 # Return

 * `bool` - true if the client securely connected with the auth protocol, false otherwise.

 # Example
 ```js
 #{
     authenticate: [
        action "log info" || log("info", `${is_secured()}`),
     ]
 }
 ```

 

</div>
<br/>
</details>