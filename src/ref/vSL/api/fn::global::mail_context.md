# global::mail_context



<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn add_rcpt_envelop(context: Context, new_addr: String) -> ()
```

<details>
<summary markdown="span"> details </summary>

add a recipient to the envelop.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn add_rcpt_envelop(context: Context, new_addr: SharedObject) -> ()
```

<details>
<summary markdown="span"> details </summary>

add a recipient to the envelop.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn get auth(context: Context) -> Credentials
```

<details>
<summary markdown="span"> details </summary>

Get the `auth` property of the connection.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn get authid(credentials: Credentials) -> String
```

<details>
<summary markdown="span"> details </summary>

Get the `authid` property of the connection.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn get authpass(credentials: Credentials) -> String
```

<details>
<summary markdown="span"> details </summary>

Get the `authpass` property of the connection.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn get client_address(context: Context) -> String
```

<details>
<summary markdown="span"> details </summary>

Get the peer address of the client.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn get client_ip(context: Context) -> String
```

<details>
<summary markdown="span"> details </summary>

Get the peer ip address of the client.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn get client_port(context: Context) -> int>
```

<details>
<summary markdown="span"> details </summary>

Get the peer port of the client.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn get connection_timestamp(context: Context) -> OffsetDateTime>
```

<details>
<summary markdown="span"> details </summary>

Get the timestamp when the client connected to the server.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn get helo(context: Context) -> String
```

<details>
<summary markdown="span"> details </summary>

Get the domain named introduced by the client.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn get is_authenticated(context: Context) -> bool
```

<details>
<summary markdown="span"> details </summary>

Has the connection validated the client credentials?
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn get is_secured(context: Context) -> bool
```

<details>
<summary markdown="span"> details </summary>

Is the connection under TLS?
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn get mail_from(context: Context) -> SharedObject
```

<details>
<summary markdown="span"> details </summary>

Get the `MailFrom` envelope.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn get mail_timestamp(context: Context) -> OffsetDateTime>
```

<details>
<summary markdown="span"> details </summary>

Get the timestamp when the client started to send the message.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn get message_id(context: Context) -> String
```

<details>
<summary markdown="span"> details </summary>

Get the `message_id`
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn get rcpt(context: Context) -> SharedObject
```

<details>
<summary markdown="span"> details </summary>

Get the lase element in the `RcptTo` envelope.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn get rcpt_list(context: Context) -> Array>
```

<details>
<summary markdown="span"> details </summary>

Get the `RcptTo` envelope.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn get server_address(context: Context) -> String
```

<details>
<summary markdown="span"> details </summary>

Get the server address which served this connection.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn get server_ip(context: Context) -> IpAddr>
```

<details>
<summary markdown="span"> details </summary>

Get the server ip address which served this connection.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn get server_name(context: Context) -> String
```

<details>
<summary markdown="span"> details </summary>

Get server name under which the client has been served.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn get server_port(context: Context) -> int>
```

<details>
<summary markdown="span"> details </summary>

Get the server port which served this connection.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn get type(credentials: Credentials) -> String
```

<details>
<summary markdown="span"> details </summary>

Get the type of the `auth` property of the connection.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn remove_rcpt_envelop(context: Context, addr: String) -> ()
```

<details>
<summary markdown="span"> details </summary>

remove a recipient from the envelop.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn remove_rcpt_envelop(context: Context, addr: SharedObject) -> ()
```

<details>
<summary markdown="span"> details </summary>

remove a recipient from the envelop.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn rewrite_mail_from_envelop(context: Context, new_addr: String) -> ()
```

<details>
<summary markdown="span"> details </summary>

Change the sender of the envelop.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn rewrite_mail_from_envelop(context: Context, new_addr: SharedObject) -> ()
```

<details>
<summary markdown="span"> details </summary>

Change the sender of the envelop using an object.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn rewrite_rcpt_envelop(context: Context, old_addr: SharedObject, new_addr: SharedObject) -> ()
```

<details>
<summary markdown="span"> details </summary>

Replace a recipient of the envelop.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn rewrite_rcpt_envelop(context: Context, old_addr: String, new_addr: SharedObject) -> ()
```

<details>
<summary markdown="span"> details </summary>

Replace a recipient of the envelop.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn rewrite_rcpt_envelop(context: Context, old_addr: SharedObject, new_addr: String) -> ()
```

<details>
<summary markdown="span"> details </summary>

Replace a recipient of the envelop.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn rewrite_rcpt_envelop(context: Context, old_addr: String, new_addr: String) -> ()
```

<details>
<summary markdown="span"> details </summary>

Replace a recipient of the envelop.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn to_debug(context: Server) -> String
```

<details>
<summary markdown="span"> details </summary>

Convert a `Server` to a debug string.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn to_debug(context: Context) -> String
```

<details>
<summary markdown="span"> details </summary>

Convert a `Context` to a debug string.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn to_string(_: Server) -> String
```

<details>
<summary markdown="span"> details </summary>

Convert a `Server` to a `String`.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn to_string(_: Context) -> String
```

<details>
<summary markdown="span"> details </summary>

Convert a `Context` to a `String`.
</details>

</div>
</br>

