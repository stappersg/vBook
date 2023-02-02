# global::auth

Authentication mechanisms and credential manipulation.


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> credentials </h2>

```rust,ignore
fn credentials() -> Credentials
```

<details>
<summary markdown="span"> details </summary>

Get authentication credentials from the client.

# Effective smtp stage

`authenticate` only.

# Return

* `Credentials` - the credentials of the client.

# Example

```
#{
    authenticate: [
       action "log auth" || log("info", `${auth::credentials()}`),
    ]
}
```
</details>

</div>
</br>

<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>get</code> anonymous_token </h2>

```rust,ignore
fn get anonymous_token(credentials: Credentials) -> String
```

<details>
<summary markdown="span"> details </summary>

Get the `anonymous_token` property of the connection.
Can only be use on 'AnonymousToken' authentication typed credentials.

# Effective smtp stage

`authenticate` only.

# Return

* `String` - the token.

# Examples

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
</details>

</div>
</br>

<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>get</code> authid </h2>

```rust,ignore
fn get authid(credentials: Credentials) -> String
```

<details>
<summary markdown="span"> details </summary>

Get the `authid` property of the connection.
Can only be use on 'Verify' authentication typed credentials.

# Effective smtp stage

`authenticate` only.

# Return

* `String` - the authentication id.

# Examples

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
</details>

</div>
</br>

<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>get</code> authpass </h2>

```rust,ignore
fn get authpass(credentials: Credentials) -> String
```

<details>
<summary markdown="span"> details </summary>

Get the `authpass` property of the connection.
Can only be use on 'Verify' authentication typed credentials.

# Effective smtp stage

`authenticate` only.

# Return

* `String` - the authentication password.

# Examples

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
</details>

</div>
</br>

<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>get</code> type </h2>

```rust,ignore
fn get type(credentials: Credentials) -> String
```

<details>
<summary markdown="span"> details </summary>

Get the type of the `auth` property of the connection.

# Effective smtp stage

`authenticate` only.

# Return

* `String` - the credentials type.

# Examples

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
</details>

</div>
</br>

<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> is_authenticated </h2>

```rust,ignore
fn is_authenticated() -> bool
```

<details>
<summary markdown="span"> details </summary>

Check if the client is authenticated.

# Effective smtp stage

`authenticate` stage only.

# Return

* `bool` - `true` if the client succeeded to authenticate itself, `false` otherwise.

# Example

```
#{
    authenticate: [
       action "log info" || log("info", `client authenticated: ${auth::is_authenticated()}`),
    ]
}
```
</details>

</div>
</br>

<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> unix_users </h2>

```rust,ignore
fn unix_users() -> Status
```

<details>
<summary markdown="span"> details </summary>

Process the SASL authentication mechanism.

The current implementation support "PLAIN" mechanism, and will call the
`testsaslauthd` program to check the credentials.

The credentials will be verified depending on the mode of `saslauthd`.

A native implementation will be provided in the future.
</details>

</div>
</br>
