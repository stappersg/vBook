# Auth
This module contains authentication mechanisms to secure your server.

<div style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 20px; border-radius: 5px;'>
<h2> fn <em style='color: var(--inline-code-color);'>auth</em>() </h2>
 Get authentication credentials from the client.

 ### Effective smtp stage

 `authenticate` only.

 ### Return

 * `Credentials` - the credentials of the client.

 ### Example
 ```js
 #{
     authenticate: [
        action "log info" || log("info", `${auth()}`),
     ]
 }
 ```

 

</div>
<br/>
<br/>

<div style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 20px; border-radius: 5px;'>
<h2> fn <em style='color: var(--inline-code-color);'>authenticate</em>() </h2>
 Process the SASL authentication mechanism.

 The current implementation support "PLAIN" mechanism, and will call the
 `testsaslauthd` program to check the credentials.

 The credentials will be verified depending on the mode of `saslauthd`.

 A native implementation will be provided in the future.

 

</div>
<br/>
<br/>

<div style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 20px; border-radius: 5px;'>
<h2> fn <em style='color: var(--inline-code-color);'>is_authenticated</em>() </h2>
 Check if the client is authenticated.

 ### Effective smtp stage

 `authenticate` only.

 ### Return

 * `bool` - true if the client succeeded to authenticate itself, false otherwise.

 ### Example
 ```js
 #{
     authenticate: [
        action "log info" || log("info", `${is_authenticated()}`),
     ]
 }
 ```

 

</div>
<br/>
<br/>

<div style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 20px; border-radius: 5px;'>
<h2> fn <em style='color: var(--inline-code-color);'>is_secured</em>() </h2>
 Has the connection been secured under the encryption protocol SSL/TLS

 ### Effective smtp stage

 all

 ### Return

 * boolean value (`true` if the connection is secured, `false` otherwise)

 ### Example
 ```js
 #{
   mail: [
     action "log ssl/tls" || {
       log("info", `My client is ${if is_secured() { "secured" } else { "unsecured!!!" }}`)
     }
   ]
 }
 ```

 

</div>
<br/>
<br/>