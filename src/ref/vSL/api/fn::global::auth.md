# global::auth

Authentication mechanisms and credential manipulation.


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> unix_users </h2>

```rust,ignore
fn unix_users() -> Status
```

<div class="tab">
    <button
    group="unix_users"
    id="link-unix_users-description"
    class="tablinks active"
    onclick="openTab(event, 'unix_users', 'description')">
        Description
    </button></div>

<div group="unix_users" id="unix_users-description" style="display: block;" markdown="span" class="tabcontent">
Process the SASL authentication mechanism.

The current implementation support "PLAIN" mechanism, and will call the
`testsaslauthd` program to check the credentials.

The credentials will be verified depending on the mode of `saslauthd`.

A native implementation will be provided in the future.
</div>

</div>
</br>

<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> is_authenticated </h2>

```rust,ignore
fn is_authenticated() -> bool
```

<div class="tab">
    <button
    group="is_authenticated"
    id="link-is_authenticated-description"
    class="tablinks active"
    onclick="openTab(event, 'is_authenticated', 'description')">
        Description
    </button>
    <button
    group="is_authenticated"
    id="link-is_authenticated-Effective smtp stage"
    class="tablinks"
    onclick="openTab(event, 'is_authenticated', 'Effective smtp stage')">
        Effective smtp stage
    </button>
    <button
    group="is_authenticated"
    id="link-is_authenticated-Return"
    class="tablinks"
    onclick="openTab(event, 'is_authenticated', 'Return')">
        Return
    </button>
    <button
    group="is_authenticated"
    id="link-is_authenticated-Example"
    class="tablinks"
    onclick="openTab(event, 'is_authenticated', 'Example')">
        Example
    </button></div>

<div group="is_authenticated" id="is_authenticated-description" style="display: block;" markdown="span" class="tabcontent">
Check if the client is authenticated.


</div>

<div group="is_authenticated" id="is_authenticated-Effective smtp stage" class="tabcontent">

`authenticate` stage only.


</div>

<div group="is_authenticated" id="is_authenticated-Return" class="tabcontent">

* `bool` - `true` if the client succeeded to authenticate itself, `false` otherwise.


</div>

<div group="is_authenticated" id="is_authenticated-Example" class="tabcontent">

```
#{
    authenticate: [
       action "log info" || log("info", `client authenticated: ${auth::is_authenticated()}`),
    ]
}
```
</div>

</div>
</br>

<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> credentials </h2>

```rust,ignore
fn credentials() -> Credentials
```

<div class="tab">
    <button
    group="credentials"
    id="link-credentials-description"
    class="tablinks active"
    onclick="openTab(event, 'credentials', 'description')">
        Description
    </button>
    <button
    group="credentials"
    id="link-credentials-Effective smtp stage"
    class="tablinks"
    onclick="openTab(event, 'credentials', 'Effective smtp stage')">
        Effective smtp stage
    </button>
    <button
    group="credentials"
    id="link-credentials-Return"
    class="tablinks"
    onclick="openTab(event, 'credentials', 'Return')">
        Return
    </button>
    <button
    group="credentials"
    id="link-credentials-Example"
    class="tablinks"
    onclick="openTab(event, 'credentials', 'Example')">
        Example
    </button></div>

<div group="credentials" id="credentials-description" style="display: block;" markdown="span" class="tabcontent">
Get authentication credentials from the client.


</div>

<div group="credentials" id="credentials-Effective smtp stage" class="tabcontent">

`authenticate` only.


</div>

<div group="credentials" id="credentials-Return" class="tabcontent">

* `Credentials` - the credentials of the client.


</div>

<div group="credentials" id="credentials-Example" class="tabcontent">

```
#{
    authenticate: [
       action "log auth" || log("info", `${auth::credentials()}`),
    ]
}
```
</div>

</div>
</br>

<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>get</code> type </h2>

```rust,ignore
fn get type(credentials: Credentials) -> String
```

<div class="tab">
    <button
    group="get$type"
    id="link-get$type-description"
    class="tablinks active"
    onclick="openTab(event, 'get$type', 'description')">
        Description
    </button>
    <button
    group="get$type"
    id="link-get$type-Effective smtp stage"
    class="tablinks"
    onclick="openTab(event, 'get$type', 'Effective smtp stage')">
        Effective smtp stage
    </button>
    <button
    group="get$type"
    id="link-get$type-Return"
    class="tablinks"
    onclick="openTab(event, 'get$type', 'Return')">
        Return
    </button>
    <button
    group="get$type"
    id="link-get$type-Examples"
    class="tablinks"
    onclick="openTab(event, 'get$type', 'Examples')">
        Examples
    </button></div>

<div group="get$type" id="get$type-description" style="display: block;" markdown="span" class="tabcontent">
Get the type of the `auth` property of the connection.


</div>

<div group="get$type" id="get$type-Effective smtp stage" class="tabcontent">

`authenticate` only.


</div>

<div group="get$type" id="get$type-Return" class="tabcontent">

* `String` - the credentials type.


</div>

<div group="get$type" id="get$type-Examples" class="tabcontent">

```
#{
    authenticate: [
       action "log auth type" || {
            let credentials = auth::credentials();

            // Logs here will output 'Verify' or 'AnonymousToken'.
            // depending on the authentication type.
            log("info", `credentials type: ${credentials.type}`);
        },
    ]
}
```
</div>

</div>
</br>

<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>get</code> authid </h2>

```rust,ignore
fn get authid(credentials: Credentials) -> String
```

<div class="tab">
    <button
    group="get$authid"
    id="link-get$authid-description"
    class="tablinks active"
    onclick="openTab(event, 'get$authid', 'description')">
        Description
    </button>
    <button
    group="get$authid"
    id="link-get$authid-Effective smtp stage"
    class="tablinks"
    onclick="openTab(event, 'get$authid', 'Effective smtp stage')">
        Effective smtp stage
    </button>
    <button
    group="get$authid"
    id="link-get$authid-Return"
    class="tablinks"
    onclick="openTab(event, 'get$authid', 'Return')">
        Return
    </button>
    <button
    group="get$authid"
    id="link-get$authid-Examples"
    class="tablinks"
    onclick="openTab(event, 'get$authid', 'Examples')">
        Examples
    </button></div>

<div group="get$authid" id="get$authid-description" style="display: block;" markdown="span" class="tabcontent">
Get the `authid` property of the connection.
Can only be use on 'Verify' authentication typed credentials.


</div>

<div group="get$authid" id="get$authid-Effective smtp stage" class="tabcontent">

`authenticate` only.


</div>

<div group="get$authid" id="get$authid-Return" class="tabcontent">

* `String` - the authentication id.


</div>

<div group="get$authid" id="get$authid-Examples" class="tabcontent">

```
#{
    authenticate: [
       action "log auth id" || {
            let credentials = auth::credentials();
            log("info", `credentials id: ${credentials.authid}`);
        },
    ]
}
```
</div>

</div>
</br>

<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>get</code> authpass </h2>

```rust,ignore
fn get authpass(credentials: Credentials) -> String
```

<div class="tab">
    <button
    group="get$authpass"
    id="link-get$authpass-description"
    class="tablinks active"
    onclick="openTab(event, 'get$authpass', 'description')">
        Description
    </button>
    <button
    group="get$authpass"
    id="link-get$authpass-Effective smtp stage"
    class="tablinks"
    onclick="openTab(event, 'get$authpass', 'Effective smtp stage')">
        Effective smtp stage
    </button>
    <button
    group="get$authpass"
    id="link-get$authpass-Return"
    class="tablinks"
    onclick="openTab(event, 'get$authpass', 'Return')">
        Return
    </button>
    <button
    group="get$authpass"
    id="link-get$authpass-Examples"
    class="tablinks"
    onclick="openTab(event, 'get$authpass', 'Examples')">
        Examples
    </button></div>

<div group="get$authpass" id="get$authpass-description" style="display: block;" markdown="span" class="tabcontent">
Get the `authpass` property of the connection.
Can only be use on 'Verify' authentication typed credentials.


</div>

<div group="get$authpass" id="get$authpass-Effective smtp stage" class="tabcontent">

`authenticate` only.


</div>

<div group="get$authpass" id="get$authpass-Return" class="tabcontent">

* `String` - the authentication password.


</div>

<div group="get$authpass" id="get$authpass-Examples" class="tabcontent">

```
#{
    authenticate: [
       action "log auth pass" || {
            let credentials = auth::credentials();
            log("info", `credentials pass: ${credentials.authpass}`);
        },
    ]
}
```
</div>

</div>
</br>

<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>get</code> anonymous_token </h2>

```rust,ignore
fn get anonymous_token(credentials: Credentials) -> String
```

<div class="tab">
    <button
    group="get$anonymous_token"
    id="link-get$anonymous_token-description"
    class="tablinks active"
    onclick="openTab(event, 'get$anonymous_token', 'description')">
        Description
    </button>
    <button
    group="get$anonymous_token"
    id="link-get$anonymous_token-Effective smtp stage"
    class="tablinks"
    onclick="openTab(event, 'get$anonymous_token', 'Effective smtp stage')">
        Effective smtp stage
    </button>
    <button
    group="get$anonymous_token"
    id="link-get$anonymous_token-Return"
    class="tablinks"
    onclick="openTab(event, 'get$anonymous_token', 'Return')">
        Return
    </button>
    <button
    group="get$anonymous_token"
    id="link-get$anonymous_token-Examples"
    class="tablinks"
    onclick="openTab(event, 'get$anonymous_token', 'Examples')">
        Examples
    </button></div>

<div group="get$anonymous_token" id="get$anonymous_token-description" style="display: block;" markdown="span" class="tabcontent">
Get the `anonymous_token` property of the connection.
Can only be use on 'AnonymousToken' authentication typed credentials.


</div>

<div group="get$anonymous_token" id="get$anonymous_token-Effective smtp stage" class="tabcontent">

`authenticate` only.


</div>

<div group="get$anonymous_token" id="get$anonymous_token-Return" class="tabcontent">

* `String` - the token.


</div>

<div group="get$anonymous_token" id="get$anonymous_token-Examples" class="tabcontent">

```
#{
    authenticate: [
       action "log auth token" || {
            let credentials = auth::credentials();
            log("info", `credentials token: ${credentials.anonymous_token}`);
        },
    ]
}
```
</div>

</div>
</br>
