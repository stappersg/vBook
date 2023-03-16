# global::ctx

Inspect the transaction context.


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> to_string </h2>

```rust,ignore
fn to_string(context: Context) -> String
```

<div class="tab">
    <button
    group="to_string"
    id="link-to_string-description"
    class="tablinks active"
    onclick="openTab(event, 'to_string', 'description')">
        Description
    </button></div>

<div group="to_string" id="to_string-description" style="display: block;" markdown="span" class="tabcontent">
Produce a serialized JSON representation of the mail context.
</div>

</div>
</br>

<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> client_address </h2>

```rust,ignore
fn client_address() -> String
```

<div class="tab">
    <button
    group="client_address"
    id="link-client_address-description"
    class="tablinks active"
    onclick="openTab(event, 'client_address', 'description')">
        Description
    </button>
    <button
    group="client_address"
    id="link-client_address-Effective smtp stage"
    class="tablinks"
    onclick="openTab(event, 'client_address', 'Effective smtp stage')">
        Effective smtp stage
    </button>
    <button
    group="client_address"
    id="link-client_address-Return"
    class="tablinks"
    onclick="openTab(event, 'client_address', 'Return')">
        Return
    </button>
    <button
    group="client_address"
    id="link-client_address-Examples"
    class="tablinks"
    onclick="openTab(event, 'client_address', 'Examples')">
        Examples
    </button></div>

<div group="client_address" id="client_address-description" style="display: block;" markdown="span" class="tabcontent">
Get the address of the client.


</div>

<div group="client_address" id="client_address-Effective smtp stage" class="tabcontent">

All of them.


</div>

<div group="client_address" id="client_address-Return" class="tabcontent">

* `string` - the client's address with the `ip:port` format.


</div>

<div group="client_address" id="client_address-Examples" class="tabcontent">

```
#{
  connect: [
    action "log client address" || {
      log("info", `new client: ${ctx::client_address()}`);
    },
  ],
}
```
</div>

</div>
</br>

<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> client_ip </h2>

```rust,ignore
fn client_ip() -> String
```

<div class="tab">
    <button
    group="client_ip"
    id="link-client_ip-description"
    class="tablinks active"
    onclick="openTab(event, 'client_ip', 'description')">
        Description
    </button>
    <button
    group="client_ip"
    id="link-client_ip-Effective smtp stage"
    class="tablinks"
    onclick="openTab(event, 'client_ip', 'Effective smtp stage')">
        Effective smtp stage
    </button>
    <button
    group="client_ip"
    id="link-client_ip-Return"
    class="tablinks"
    onclick="openTab(event, 'client_ip', 'Return')">
        Return
    </button>
    <button
    group="client_ip"
    id="link-client_ip-Example"
    class="tablinks"
    onclick="openTab(event, 'client_ip', 'Example')">
        Example
    </button></div>

<div group="client_ip" id="client_ip-description" style="display: block;" markdown="span" class="tabcontent">
Get the ip address of the client.


</div>

<div group="client_ip" id="client_ip-Effective smtp stage" class="tabcontent">

All of them.


</div>

<div group="client_ip" id="client_ip-Return" class="tabcontent">

* `string` - the client's ip address.


</div>

<div group="client_ip" id="client_ip-Example" class="tabcontent">

```
#{
  connect: [
    action "log client ip" || {
      log("info", `new client: ${ctx::client_ip()}`);
    },
  ],
}
```
</div>

</div>
</br>

<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> client_port </h2>

```rust,ignore
fn client_port() -> int
```

<div class="tab">
    <button
    group="client_port"
    id="link-client_port-description"
    class="tablinks active"
    onclick="openTab(event, 'client_port', 'description')">
        Description
    </button>
    <button
    group="client_port"
    id="link-client_port-Effective smtp stage"
    class="tablinks"
    onclick="openTab(event, 'client_port', 'Effective smtp stage')">
        Effective smtp stage
    </button>
    <button
    group="client_port"
    id="link-client_port-Return"
    class="tablinks"
    onclick="openTab(event, 'client_port', 'Return')">
        Return
    </button>
    <button
    group="client_port"
    id="link-client_port-Example"
    class="tablinks"
    onclick="openTab(event, 'client_port', 'Example')">
        Example
    </button></div>

<div group="client_port" id="client_port-description" style="display: block;" markdown="span" class="tabcontent">
Get the ip port of the client.


</div>

<div group="client_port" id="client_port-Effective smtp stage" class="tabcontent">

All of them.


</div>

<div group="client_port" id="client_port-Return" class="tabcontent">

* `int` - the client's port.


</div>

<div group="client_port" id="client_port-Example" class="tabcontent">

```
#{
  connect: [
    action "log client address" || {
      log("info", `new client: ${ctx::client_ip()}:${ctx::client_port()}`);
    },
  ],
}
```
</div>

</div>
</br>

<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> server_address </h2>

```rust,ignore
fn server_address() -> String
```

<div class="tab">
    <button
    group="server_address"
    id="link-server_address-description"
    class="tablinks active"
    onclick="openTab(event, 'server_address', 'description')">
        Description
    </button>
    <button
    group="server_address"
    id="link-server_address-Effective smtp stage"
    class="tablinks"
    onclick="openTab(event, 'server_address', 'Effective smtp stage')">
        Effective smtp stage
    </button>
    <button
    group="server_address"
    id="link-server_address-Return"
    class="tablinks"
    onclick="openTab(event, 'server_address', 'Return')">
        Return
    </button>
    <button
    group="server_address"
    id="link-server_address-Example"
    class="tablinks"
    onclick="openTab(event, 'server_address', 'Example')">
        Example
    </button></div>

<div group="server_address" id="server_address-description" style="display: block;" markdown="span" class="tabcontent">
Get the full server address.


</div>

<div group="server_address" id="server_address-Effective smtp stage" class="tabcontent">

All of them.


</div>

<div group="server_address" id="server_address-Return" class="tabcontent">

* `string` - the server's address with the `ip:port` format.


</div>

<div group="server_address" id="server_address-Example" class="tabcontent">

```
#{
  connect: [
    action "log server address" || {
      log("info", `server: ${ctx::server_address()}`);
    },
  ],
}
```
</div>

</div>
</br>

<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> server_ip </h2>

```rust,ignore
fn server_ip() -> String
```

<div class="tab">
    <button
    group="server_ip"
    id="link-server_ip-description"
    class="tablinks active"
    onclick="openTab(event, 'server_ip', 'description')">
        Description
    </button>
    <button
    group="server_ip"
    id="link-server_ip-Effective smtp stage"
    class="tablinks"
    onclick="openTab(event, 'server_ip', 'Effective smtp stage')">
        Effective smtp stage
    </button>
    <button
    group="server_ip"
    id="link-server_ip-Return"
    class="tablinks"
    onclick="openTab(event, 'server_ip', 'Return')">
        Return
    </button>
    <button
    group="server_ip"
    id="link-server_ip-Example"
    class="tablinks"
    onclick="openTab(event, 'server_ip', 'Example')">
        Example
    </button></div>

<div group="server_ip" id="server_ip-description" style="display: block;" markdown="span" class="tabcontent">
Get the server's ip.


</div>

<div group="server_ip" id="server_ip-Effective smtp stage" class="tabcontent">

All of them.


</div>

<div group="server_ip" id="server_ip-Return" class="tabcontent">

* `string` - the server's ip.


</div>

<div group="server_ip" id="server_ip-Example" class="tabcontent">

```
#{
  connect: [
    action "log server ip" || {
      log("info", `server: ${ctx::server_ip()}`);
    },
  ],
}
```
</div>

</div>
</br>

<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> server_port </h2>

```rust,ignore
fn server_port() -> int
```

<div class="tab">
    <button
    group="server_port"
    id="link-server_port-description"
    class="tablinks active"
    onclick="openTab(event, 'server_port', 'description')">
        Description
    </button>
    <button
    group="server_port"
    id="link-server_port-Effective smtp stage"
    class="tablinks"
    onclick="openTab(event, 'server_port', 'Effective smtp stage')">
        Effective smtp stage
    </button>
    <button
    group="server_port"
    id="link-server_port-Return"
    class="tablinks"
    onclick="openTab(event, 'server_port', 'Return')">
        Return
    </button>
    <button
    group="server_port"
    id="link-server_port-Example"
    class="tablinks"
    onclick="openTab(event, 'server_port', 'Example')">
        Example
    </button></div>

<div group="server_port" id="server_port-description" style="display: block;" markdown="span" class="tabcontent">
Get the server's port.


</div>

<div group="server_port" id="server_port-Effective smtp stage" class="tabcontent">

All of them.


</div>

<div group="server_port" id="server_port-Return" class="tabcontent">

* `string` - the server's port.


</div>

<div group="server_port" id="server_port-Example" class="tabcontent">

```
#{
  connect: [
    action "log server address" || {
      log("info", `server: ${ctx::server_ip()}:${ctx::server_port()}`);
    },
  ],
}
```
</div>

</div>
</br>

<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> connection_timestamp </h2>

```rust,ignore
fn connection_timestamp() -> OffsetDateTime
```

<div class="tab">
    <button
    group="connection_timestamp"
    id="link-connection_timestamp-description"
    class="tablinks active"
    onclick="openTab(event, 'connection_timestamp', 'description')">
        Description
    </button>
    <button
    group="connection_timestamp"
    id="link-connection_timestamp-Effective smtp stage"
    class="tablinks"
    onclick="openTab(event, 'connection_timestamp', 'Effective smtp stage')">
        Effective smtp stage
    </button>
    <button
    group="connection_timestamp"
    id="link-connection_timestamp-Return"
    class="tablinks"
    onclick="openTab(event, 'connection_timestamp', 'Return')">
        Return
    </button>
    <button
    group="connection_timestamp"
    id="link-connection_timestamp-Example"
    class="tablinks"
    onclick="openTab(event, 'connection_timestamp', 'Example')">
        Example
    </button></div>

<div group="connection_timestamp" id="connection_timestamp-description" style="display: block;" markdown="span" class="tabcontent">
Get a the timestamp of the client's connection time.


</div>

<div group="connection_timestamp" id="connection_timestamp-Effective smtp stage" class="tabcontent">

All of them.


</div>

<div group="connection_timestamp" id="connection_timestamp-Return" class="tabcontent">

* `timestamp` - the connection timestamp of the client.


</div>

<div group="connection_timestamp" id="connection_timestamp-Example" class="tabcontent">

```
#{
  connect: [
    action "log client" || {
      log("info", `new client connected at ${ctx::connection_timestamp()}`);
    },
  ],
}
```
</div>

</div>
</br>

<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> server_name </h2>

```rust,ignore
fn server_name() -> String
```

<div class="tab">
    <button
    group="server_name"
    id="link-server_name-description"
    class="tablinks active"
    onclick="openTab(event, 'server_name', 'description')">
        Description
    </button>
    <button
    group="server_name"
    id="link-server_name-Effective smtp stage"
    class="tablinks"
    onclick="openTab(event, 'server_name', 'Effective smtp stage')">
        Effective smtp stage
    </button>
    <button
    group="server_name"
    id="link-server_name-Return"
    class="tablinks"
    onclick="openTab(event, 'server_name', 'Return')">
        Return
    </button>
    <button
    group="server_name"
    id="link-server_name-Example"
    class="tablinks"
    onclick="openTab(event, 'server_name', 'Example')">
        Example
    </button></div>

<div group="server_name" id="server_name-description" style="display: block;" markdown="span" class="tabcontent">
Get the name of the server.


</div>

<div group="server_name" id="server_name-Effective smtp stage" class="tabcontent">

All of them.


</div>

<div group="server_name" id="server_name-Return" class="tabcontent">

* `string` - the name of the server.


</div>

<div group="server_name" id="server_name-Example" class="tabcontent">

```
#{
  connect: [
    action "log server" || {
      log("info", `server name: ${ctx::server_name()}`);
    },
  ],
}
```
</div>

</div>
</br>

<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> is_secured </h2>

```rust,ignore
fn is_secured() -> bool
```

<div class="tab">
    <button
    group="is_secured"
    id="link-is_secured-description"
    class="tablinks active"
    onclick="openTab(event, 'is_secured', 'description')">
        Description
    </button>
    <button
    group="is_secured"
    id="link-is_secured-Effective smtp stage"
    class="tablinks"
    onclick="openTab(event, 'is_secured', 'Effective smtp stage')">
        Effective smtp stage
    </button>
    <button
    group="is_secured"
    id="link-is_secured-Return"
    class="tablinks"
    onclick="openTab(event, 'is_secured', 'Return')">
        Return
    </button>
    <button
    group="is_secured"
    id="link-is_secured-Example"
    class="tablinks"
    onclick="openTab(event, 'is_secured', 'Example')">
        Example
    </button></div>

<div group="is_secured" id="is_secured-description" style="display: block;" markdown="span" class="tabcontent">
Has the connection been secured under the encryption protocol SSL/TLS.


</div>

<div group="is_secured" id="is_secured-Effective smtp stage" class="tabcontent">

all of them.


</div>

<div group="is_secured" id="is_secured-Return" class="tabcontent">

* bool - `true` if the connection is secured, `false` otherwise.


</div>

<div group="is_secured" id="is_secured-Example" class="tabcontent">

```
#{
  connect: [
    action "log ssl/tls" || {
      log("info", `The client is ${if ctx::is_secured() { "secured" } else { "unsecured!!!" }}`)
    }
  ],
}
```
</div>

</div>
</br>

<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> helo </h2>

```rust,ignore
fn helo() -> String
```

<div class="tab">
    <button
    group="helo"
    id="link-helo-description"
    class="tablinks active"
    onclick="openTab(event, 'helo', 'description')">
        Description
    </button>
    <button
    group="helo"
    id="link-helo-Effective smtp stage"
    class="tablinks"
    onclick="openTab(event, 'helo', 'Effective smtp stage')">
        Effective smtp stage
    </button>
    <button
    group="helo"
    id="link-helo-Return"
    class="tablinks"
    onclick="openTab(event, 'helo', 'Return')">
        Return
    </button>
    <button
    group="helo"
    id="link-helo-Examples"
    class="tablinks"
    onclick="openTab(event, 'helo', 'Examples')">
        Examples
    </button></div>

<div group="helo" id="helo-description" style="display: block;" markdown="span" class="tabcontent">
Get the value of the `HELO/EHLO` command sent by the client.


</div>

<div group="helo" id="helo-Effective smtp stage" class="tabcontent">

`helo` and onwards.


</div>

<div group="helo" id="helo-Return" class="tabcontent">

* `string` - the value of the `HELO/EHLO` command.


</div>

<div group="helo" id="helo-Examples" class="tabcontent">

```
#{
    helo: [
       action "log info" || log("info", `helo/ehlo value: ${ctx::helo()}`),
    ]
}
```
</div>

</div>
</br>

<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> mail_from </h2>

```rust,ignore
fn mail_from() -> SharedObject
```

<div class="tab">
    <button
    group="mail_from"
    id="link-mail_from-description"
    class="tablinks active"
    onclick="openTab(event, 'mail_from', 'description')">
        Description
    </button>
    <button
    group="mail_from"
    id="link-mail_from-Effective smtp stage"
    class="tablinks"
    onclick="openTab(event, 'mail_from', 'Effective smtp stage')">
        Effective smtp stage
    </button>
    <button
    group="mail_from"
    id="link-mail_from-Return"
    class="tablinks"
    onclick="openTab(event, 'mail_from', 'Return')">
        Return
    </button>
    <button
    group="mail_from"
    id="link-mail_from-Examples"
    class="tablinks"
    onclick="openTab(event, 'mail_from', 'Examples')">
        Examples
    </button></div>

<div group="mail_from" id="mail_from-description" style="display: block;" markdown="span" class="tabcontent">
Get the value of the `MAIL FROM` command sent by the client.


</div>

<div group="mail_from" id="mail_from-Effective smtp stage" class="tabcontent">

`mail` and onwards.

</div>

<div group="mail_from" id="mail_from-Return" class="tabcontent">

* `address` - the sender address.


</div>

<div group="mail_from" id="mail_from-Examples" class="tabcontent">

```
#{
    helo: [
       action "log info" || log("info", `received sender: ${ctx::mail_from()}`),
    ]
}
```
</div>

</div>
</br>

<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> rcpt_list </h2>

```rust,ignore
fn rcpt_list() -> Array
```

<div class="tab">
    <button
    group="rcpt_list"
    id="link-rcpt_list-description"
    class="tablinks active"
    onclick="openTab(event, 'rcpt_list', 'description')">
        Description
    </button>
    <button
    group="rcpt_list"
    id="link-rcpt_list-Effective smtp stage"
    class="tablinks"
    onclick="openTab(event, 'rcpt_list', 'Effective smtp stage')">
        Effective smtp stage
    </button>
    <button
    group="rcpt_list"
    id="link-rcpt_list-Return"
    class="tablinks"
    onclick="openTab(event, 'rcpt_list', 'Return')">
        Return
    </button>
    <button
    group="rcpt_list"
    id="link-rcpt_list-Examples"
    class="tablinks"
    onclick="openTab(event, 'rcpt_list', 'Examples')">
        Examples
    </button></div>

<div group="rcpt_list" id="rcpt_list-description" style="display: block;" markdown="span" class="tabcontent">
Get the list of recipients received by the client.


</div>

<div group="rcpt_list" id="rcpt_list-Effective smtp stage" class="tabcontent">

`rcpt` and onwards. Note that you will not have all recipients received
all at once in the `rcpt` stage. It is better to use this function
in the later stages.


</div>

<div group="rcpt_list" id="rcpt_list-Return" class="tabcontent">

* `Array of addresses` - the list containing all recipients.


</div>

<div group="rcpt_list" id="rcpt_list-Examples" class="tabcontent">

```
#{
    preq: [
       action "log recipients" || log("info", `recipients: ${ctx::rcpt_list()}`),
    ]
}
```
</div>

</div>
</br>

<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> rcpt </h2>

```rust,ignore
fn rcpt() -> SharedObject
```

<div class="tab">
    <button
    group="rcpt"
    id="link-rcpt-description"
    class="tablinks active"
    onclick="openTab(event, 'rcpt', 'description')">
        Description
    </button>
    <button
    group="rcpt"
    id="link-rcpt-Effective smtp stage"
    class="tablinks"
    onclick="openTab(event, 'rcpt', 'Effective smtp stage')">
        Effective smtp stage
    </button>
    <button
    group="rcpt"
    id="link-rcpt-Return"
    class="tablinks"
    onclick="openTab(event, 'rcpt', 'Return')">
        Return
    </button>
    <button
    group="rcpt"
    id="link-rcpt-Examples"
    class="tablinks"
    onclick="openTab(event, 'rcpt', 'Examples')">
        Examples
    </button></div>

<div group="rcpt" id="rcpt-description" style="display: block;" markdown="span" class="tabcontent">
Get the value of the current `RCPT TO` command sent by the client.


</div>

<div group="rcpt" id="rcpt-Effective smtp stage" class="tabcontent">

`rcpt` and onwards. Please note that `ctx::rcpt()` will always return
the last recipient received in stages after the `rcpt` stage. Therefore,
this functions is best used in the `rcpt` stage.


</div>

<div group="rcpt" id="rcpt-Return" class="tabcontent">

* `address` - the address of the received recipient.


</div>

<div group="rcpt" id="rcpt-Examples" class="tabcontent">

```
#{
    rcpt: [
       action "log recipients" || log("info", `new recipient: ${ctx::rcpt()}`),
    ]
}
```
</div>

</div>
</br>

<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> mail_timestamp </h2>

```rust,ignore
fn mail_timestamp() -> OffsetDateTime
```

<div class="tab">
    <button
    group="mail_timestamp"
    id="link-mail_timestamp-description"
    class="tablinks active"
    onclick="openTab(event, 'mail_timestamp', 'description')">
        Description
    </button>
    <button
    group="mail_timestamp"
    id="link-mail_timestamp-Effective smtp stage"
    class="tablinks"
    onclick="openTab(event, 'mail_timestamp', 'Effective smtp stage')">
        Effective smtp stage
    </button>
    <button
    group="mail_timestamp"
    id="link-mail_timestamp-Return"
    class="tablinks"
    onclick="openTab(event, 'mail_timestamp', 'Return')">
        Return
    </button>
    <button
    group="mail_timestamp"
    id="link-mail_timestamp-Examples"
    class="tablinks"
    onclick="openTab(event, 'mail_timestamp', 'Examples')">
        Examples
    </button></div>

<div group="mail_timestamp" id="mail_timestamp-description" style="display: block;" markdown="span" class="tabcontent">
Get the time of reception of the email.


</div>

<div group="mail_timestamp" id="mail_timestamp-Effective smtp stage" class="tabcontent">

`preq` and onwards.


</div>

<div group="mail_timestamp" id="mail_timestamp-Return" class="tabcontent">

* `string` - the timestamp.


</div>

<div group="mail_timestamp" id="mail_timestamp-Examples" class="tabcontent">

```
#{
    preq: [
       action "receiving the email" || log("info", `time of reception: ${ctx::mail_timestamp()}`),
    ]
}
```
</div>

</div>
</br>

<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> message_id </h2>

```rust,ignore
fn message_id() -> String
```

<div class="tab">
    <button
    group="message_id"
    id="link-message_id-description"
    class="tablinks active"
    onclick="openTab(event, 'message_id', 'description')">
        Description
    </button>
    <button
    group="message_id"
    id="link-message_id-Effective smtp stage"
    class="tablinks"
    onclick="openTab(event, 'message_id', 'Effective smtp stage')">
        Effective smtp stage
    </button>
    <button
    group="message_id"
    id="link-message_id-Return"
    class="tablinks"
    onclick="openTab(event, 'message_id', 'Return')">
        Return
    </button>
    <button
    group="message_id"
    id="link-message_id-Examples"
    class="tablinks"
    onclick="openTab(event, 'message_id', 'Examples')">
        Examples
    </button></div>

<div group="message_id" id="message_id-description" style="display: block;" markdown="span" class="tabcontent">
Get the unique id of the received message.


</div>

<div group="message_id" id="message_id-Effective smtp stage" class="tabcontent">

`preq` and onwards.


</div>

<div group="message_id" id="message_id-Return" class="tabcontent">

* `string` - the message id.


</div>

<div group="message_id" id="message_id-Examples" class="tabcontent">

```
#{
    preq: [
       action "message received" || log("info", `message id: ${ctx::message_id()}`),
    ]
}
```
</div>

</div>
</br>
