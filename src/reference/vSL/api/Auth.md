# Auth
## This module contains authentication mechanisms to secure your server.
<details><summary>auth()</summary><br/> Get authentication credentials from the client.

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

 
</details>
<details><summary>is_authenticated()</summary><br/> Check if the client is authenticated.

 # Effective smtp stage

 `authenticate` only.

 # Return

 * `bool` - true if the client succedded to authenticate itself, false otherwise.

 # Example
 ```js
 #{
     authenticate: [
        action "log info" || log("info", `${is_authenticated()}`),
     ]
 }
 ```

 
</details>
<details><summary>is_secured()</summary><br/> Check if the client's connexion was secure.

 # Effective smtp stage

 `authenticate` only.

 # Return

 * `bool` - true if the client securly connected with the auth protocol, false otherwise.

 # Example
 ```js
 #{
     authenticate: [
        action "log info" || log("info", `${is_secured()}`),
     ]
 }
 ```

 
</details>