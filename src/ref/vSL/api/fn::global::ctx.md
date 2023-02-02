# global::ctx

Inspect the transaction context.


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> client_address </h2>

```rust,ignore
fn client_address() -> String
```

<details>
<summary markdown="span"> details </summary>

Get the address of the client.

# Effective smtp stage

All of them.

# Return

* `string` - the client's address with the `ip:port` format.

# Examples

```
#{
  connect: [
    action "log client address" || {
      log("info", `new client: ${ctx::client_address()}`);
    },
  ],
}
```
</details>

</div>
</br>

<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> client_ip </h2>

```rust,ignore
fn client_ip() -> String
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
    action "log client ip" || {
      log("info", `new client: ${ctx::client_ip()}`);
    },
  ],
}
```
</details>

</div>
</br>

<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> client_port </h2>

```rust,ignore
fn client_port() -> int
```

<details>
<summary markdown="span"> details </summary>

Get the ip port of the client.

# Effective smtp stage

All of them.

# Return

* `int` - the client's port.

# Example

```
#{
  connect: [
    action "log client address" || {
      log("info", `new client: ${ctx::client_ip()}:${ctx::client_port()}`);
    },
  ],
}
```
</details>

</div>
</br>

<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> connection_timestamp </h2>

```rust,ignore
fn connection_timestamp() -> OffsetDateTime
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
    action "log client" || {
      log("info", `new client connected at ${ctx::connection_timestamp()}`);
    },
  ],
}
```
</details>

</div>
</br>

<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> helo </h2>

```rust,ignore
fn helo() -> String
```

<details>
<summary markdown="span"> details </summary>

Get the value of the `HELO/EHLO` command sent by the client.

# Effective smtp stage

`helo` and onwards.

# Return

* `string` - the value of the `HELO/EHLO` command.

# Examples

```
#{
    helo: [
       action "log info" || log("info", `helo/ehlo value: ${ctx::helo()}`),
    ]
}
```
</details>

</div>
</br>

<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> is_secured </h2>

```rust,ignore
fn is_secured() -> bool
```

<details>
<summary markdown="span"> details </summary>

Has the connection been secured under the encryption protocol SSL/TLS.

# Effective smtp stage

all of them.

# Return

* bool - `true` if the connection is secured, `false` otherwise.

# Example

```
#{
  connect: [
    action "log ssl/tls" || {
      log("info", `The client is ${if ctx::is_secured() { "secured" } else { "unsecured!!!" }}`)
    }
  ],
}
```
</details>

</div>
</br>

<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> mail_from </h2>

```rust,ignore
fn mail_from() -> SharedObject
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
       action "log info" || log("info", `received sender: ${ctx::mail_from()}`),
    ]
}
```
</details>

</div>
</br>

<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> mail_timestamp </h2>

```rust,ignore
fn mail_timestamp() -> OffsetDateTime
```

<details>
<summary markdown="span"> details </summary>

Get the time of reception of the email.

# Effective smtp stage

`preq` and onwards.

# Return

* `string` - the timestamp.

# Examples

```
#{
    preq: [
       action "receiving the email" || log("info", `time of reception: ${ctx::mail_timestamp()}`),
    ]
}
```
</details>

</div>
</br>

<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> message_id </h2>

```rust,ignore
fn message_id() -> String
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
       action "message received" || log("info", `message id: ${ctx::message_id()}`),
    ]
}
```
</details>

</div>
</br>

<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> rcpt </h2>

```rust,ignore
fn rcpt() -> SharedObject
```

<details>
<summary markdown="span"> details </summary>

Get the value of the current `RCPT TO` command sent by the client.

# Effective smtp stage

`rcpt` and onwards. Please note that `ctx::rcpt()` will always return
the last recipient received in stages after the `rcpt` stage. Therefore,
this functions is best used in the `rcpt` stage.

# Return

* `address` - the address of the received recipient.

# Examples

```
#{
    rcpt: [
       action "log recipients" || log("info", `new recipient: ${ctx::rcpt()}`),
    ]
}
```
</details>

</div>
</br>

<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> rcpt_list </h2>

```rust,ignore
fn rcpt_list() -> Array
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
       action "log recipients" || log("info", `recipients: ${ctx::rcpt_list()}`),
    ]
}
```
</details>

</div>
</br>

<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> server_address </h2>

```rust,ignore
fn server_address() -> String
```

<details>
<summary markdown="span"> details </summary>

Get the full server address.

# Effective smtp stage

All of them.

# Return

* `string` - the server's address with the `ip:port` format.

# Example

```
#{
  connect: [
    action "log server address" || {
      log("info", `server: ${ctx::server_address()}`);
    },
  ],
}
```
</details>

</div>
</br>

<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> server_ip </h2>

```rust,ignore
fn server_ip() -> String
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
    action "log server ip" || {
      log("info", `server: ${ctx::server_ip()}`);
    },
  ],
}
```
</details>

</div>
</br>

<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> server_name </h2>

```rust,ignore
fn server_name() -> String
```

<details>
<summary markdown="span"> details </summary>

Get the name of the server.

# Effective smtp stage

All of them.

# Return

* `string` - the name of the server.

# Example

```
#{
  connect: [
    action "log server" || {
      log("info", `server name: ${ctx::server_name()}`);
    },
  ],
}
```
</details>

</div>
</br>

<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> server_port </h2>

```rust,ignore
fn server_port() -> int
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
    action "log server address" || {
      log("info", `server: ${ctx::server_ip()}:${ctx::server_port()}`);
    },
  ],
}
```
</details>

</div>
</br>

<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> to_string </h2>

```rust,ignore
fn to_string(context: Context) -> String
```

<details>
<summary markdown="span"> details </summary>

Produce a serialized JSON representation of the mail context.
</details>

</div>
</br>
