# global::mail_context



<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> add_rcpt_envelop </h2>

```rust,ignore
fn add_rcpt_envelop(context: Context, new_addr: String) -> ()
fn add_rcpt_envelop(context: Context, new_addr: SharedObject) -> ()
```

<details>
<summary markdown="span"> details </summary>

Add a new recipient to the envelop. Note that this does not add
the recipient to the `To` header. Use `add_rcpt_message` for that.

# Args

* `rcpt` - the new recipient to add.

# Effective smtp stage

All of them.

# Examples

```
#{
    connect: [
       // always deliver a copy of the message to "john.doe@example.com".
       action "rewrite envelop" || add_rcpt_envelop("john.doe@example.com"),
    ]
}
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> auth </h2>

```rust,ignore
fn get auth(context: Context) -> Credentials

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
       action "log info" || log("info", `${auth()}`),
    ]
}
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> authpass </h2>

```rust,ignore
fn get authpass(credentials: Credentials) -> String

```

<details>
<summary markdown="span"> details </summary>

Get the `authpass` property of the connection.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> client_ip </h2>

```rust,ignore
fn get client_ip(context: Context) -> String

```

<details>
<summary markdown="span"> details </summary>

Get the ip address of the client.

# Effective smtp stage

All of them.

# Return

* `string` - the client's ip address.

# Example

```
#{
    connect: [
       action "log info" || log("info", `client ip: ${client_ip()}`),
    ]
}
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> connection_timestamp </h2>

```rust,ignore
fn get connection_timestamp(context: Context) -> OffsetDateTime

```

<details>
<summary markdown="span"> details </summary>

Get a the timestamp of the client's connection time.

# Effective smtp stage

All of them.

# Return

* `timestamp` - the connexion timestamp of the client.

# Example

```
#{
    connect: [
       action "log info" || log("info", `${connection_timestamp()}`),
    ]
}
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> is_authenticated </h2>

```rust,ignore
fn get is_authenticated(context: Context) -> bool

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
       action "log info" || log("info", `client authenticated: ${is_authenticated()}`),
    ]
}
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> mail_from </h2>

```rust,ignore
fn get mail_from(context: Context) -> SharedObject

```

<details>
<summary markdown="span"> details </summary>

Get the value of the `MAIL FROM` command sent by the client.

# Effective smtp stage

`mail` and onwards.

# Return

* `address` - the sender address.

# Examples

```
#{
    helo: [
       action "log info" || log("info", `${mail_from()}`),
    ]
}
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> message_id </h2>

```rust,ignore
fn get message_id(context: Context) -> String

```

<details>
<summary markdown="span"> details </summary>

Get the unique id of the received message.

# Effective smtp stage

`preq` and onwards.

# Return

* `string` - the message id.

# Examples

```
#{
    preq: [
       action "message received" || log("info", `message id: ${message_id()}`),
    ]
}
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> rcpt_list </h2>

```rust,ignore
fn get rcpt_list(context: Context) -> Array

```

<details>
<summary markdown="span"> details </summary>

Get the list of recipients received by the client.

# Effective smtp stage

`rcpt` and onwards. Note that you will not have all recipients received
all at once in the `rcpt` stage. It is better to use this function
in the later stages.

# Return

* `Array of addresses` - the list containing all recipients.

# Examples

```
#{
    preq: [
       action "log recipients" || log("info", `all recipients: ${rcpt_list()}`),
    ]
}
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> server_ip </h2>

```rust,ignore
fn get server_ip(context: Context) -> IpAddr

```

<details>
<summary markdown="span"> details </summary>

Get the server's ip.

# Effective smtp stage

All of them.

# Return

* `string` - the server's ip.

# Example

```
#{
    connect: [
       action "log info" || log("info", `server ip: ${server_ip()}`),
    ]
}
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> server_port </h2>

```rust,ignore
fn get server_port(context: Context) -> int

```

<details>
<summary markdown="span"> details </summary>

Get the server's port.

# Effective smtp stage

All of them.

# Return

* `string` - the server's port.

# Example
```
#{
    connect: [
       action "log info" || log("info", `server port: ${server_port()}`),
    ]
}
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> remove_rcpt_envelop </h2>

```rust,ignore
fn remove_rcpt_envelop(context: Context, addr: String) -> ()
fn remove_rcpt_envelop(context: Context, addr: SharedObject) -> ()
```

<details>
<summary markdown="span"> details </summary>

Remove a recipient from the envelop. Note that this does not remove
the recipient from the `To` header. Use `remove_rcpt_message` for that.

# Args

* `rcpt` - the recipient to remove.

# Effective smtp stage

All of them.

# Examples

```
#{
    preq: [
       // never deliver to "john.doe@example.com".
       action "rewrite envelop" || remove_rcpt_envelop("john.doe@example.com"),
    ]
}
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> rewrite_mail_from_envelop </h2>

```rust,ignore
fn rewrite_mail_from_envelop(context: Context, new_addr: String) -> ()

```

<details>
<summary markdown="span"> details </summary>

Rewrite the sender received from the `MAIL FROM` command.

# Args

* `new_addr` - the new string sender address to set.

# Effective smtp stage

`mail` and onwards.

# Examples

```
#{
    preq: [
       action "rewrite envelop" || rewrite_mail_from_envelop("unknown@example.com"),
    ]
}
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> rewrite_rcpt_envelop </h2>

```rust,ignore
fn rewrite_rcpt_envelop(context: Context, old_addr: SharedObject, new_addr: SharedObject) -> ()
fn rewrite_rcpt_envelop(context: Context, old_addr: String, new_addr: String) -> ()
fn rewrite_rcpt_envelop(context: Context, old_addr: SharedObject, new_addr: String) -> ()
```

<details>
<summary markdown="span"> details </summary>

Replace a recipient received by a `RCPT TO` command.

# Args

* `old_addr` - the recipient to replace.
* `new_addr` - the new address to use when replacing `old_addr`.

# Effective smtp stage

`rcpt` and onwards.

# Examples

```
#{
    preq: [
       action "rewrite envelop" || rewrite_rcpt_envelop(address("john.doe@example.com"), address("john.main@example.com")),
    ]
}
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> to_debug </h2>

```rust,ignore
fn to_debug(context: Context) -> String

```

<details>
<summary markdown="span"> details </summary>

Convert a `Context` to a debug string.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> to_string </h2>

```rust,ignore
fn to_string(_: Context) -> String

```

<details>
<summary markdown="span"> details </summary>

Convert a `Context` to a `String`.
</details>

</div>
</br>

