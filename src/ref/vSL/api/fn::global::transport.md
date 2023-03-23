# global::transport

Functions to configure delivery methods of emails.


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> forward </h2>

```rust,ignore
fn forward(rcpt: String, forward: SharedObject) -> ()
fn forward(rcpt: SharedObject, forward: SharedObject) -> ()
fn forward(rcpt: String, forward: String) -> ()
fn forward(rcpt: SharedObject, forward: String) -> ()
```

<div class="tab">
    <button
    group="forward"
    id="link-forward-description"
    class="tablinks active"
    onclick="openTab(event, 'forward', 'description')">
        Description
    </button>
    <button
    group="forward"
    id="link-forward-Args"
    class="tablinks"
    onclick="openTab(event, 'forward', 'Args')">
        Args
    </button>
    <button
    group="forward"
    id="link-forward-Effective smtp stage"
    class="tablinks"
    onclick="openTab(event, 'forward', 'Effective smtp stage')">
        Effective smtp stage
    </button>
    <button
    group="forward"
    id="link-forward-Examples"
    class="tablinks"
    onclick="openTab(event, 'forward', 'Examples')">
        Examples
    </button></div>

<div group="forward" id="forward-description" style="display: block;" markdown="span" class="tabcontent">
Set the delivery method to forwarding for a single recipient.
After all rules are evaluated, forwarding will be used to deliver
the email to the recipient.


</div>

<div group="forward" id="forward-Args" class="tabcontent">

* `rcpt` - the recipient to apply the method to.
* `target` - the target to forward the email to.


</div>

<div group="forward" id="forward-Effective smtp stage" class="tabcontent">

All of them.


</div>

<div group="forward" id="forward-Examples" class="tabcontent">

```
#{
    rcpt: [
      action "forward (str/str)" || {
        envelop::add_rcpt("my.address@foo.com");
        transport::forward("my.address@foo.com", "127.0.0.1");
      },
      action "forward (obj/str)" || {
        let rcpt = address("my.address@bar.com");
        envelop::add_rcpt(rcpt);
        transport::forward(rcpt, "127.0.0.2");
      },
      action "forward (str/obj)" || {
        let target = ip6("::1");
        envelop::add_rcpt("my.address@baz.com");
        transport::forward("my.address@baz.com", target);
      },
      action "forward (obj/obj)" || {
        let rcpt = address("my.address@boz.com");
        envelop::add_rcpt(rcpt);
        transport::forward(rcpt, ip4("127.0.0.4"));
      },
    ],
}
#
#
#
```

Or with url:

```
#{
    rcpt: [
      action "set forward" || {
        let user = "root@domain.tld";
        let pass = "xxxxxx";
        let host = "smtp.domain.tld";
        let port = 25;
        transport::forward_all(`smtp://${user}:${pass}@${host}:${port}?tls=opportunistic`);
      },
   ]
}
#
```
</div>

</div>
</br>

<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> forward_all </h2>

```rust,ignore
fn forward_all(forward: String) -> ()
fn forward_all(forward: SharedObject) -> ()
```

<div class="tab">
    <button
    group="forward_all"
    id="link-forward_all-description"
    class="tablinks active"
    onclick="openTab(event, 'forward_all', 'description')">
        Description
    </button>
    <button
    group="forward_all"
    id="link-forward_all-Args"
    class="tablinks"
    onclick="openTab(event, 'forward_all', 'Args')">
        Args
    </button>
    <button
    group="forward_all"
    id="link-forward_all-Effective smtp stage"
    class="tablinks"
    onclick="openTab(event, 'forward_all', 'Effective smtp stage')">
        Effective smtp stage
    </button>
    <button
    group="forward_all"
    id="link-forward_all-Examples"
    class="tablinks"
    onclick="openTab(event, 'forward_all', 'Examples')">
        Examples
    </button></div>

<div group="forward_all" id="forward_all-description" style="display: block;" markdown="span" class="tabcontent">
Set the delivery method to forwarding for all recipients.
After all rules are evaluated, forwarding will be used to deliver
the email.


</div>

<div group="forward_all" id="forward_all-Args" class="tabcontent">

* `target` - the target to forward the email to.


</div>

<div group="forward_all" id="forward_all-Effective smtp stage" class="tabcontent">

All of them.


</div>

<div group="forward_all" id="forward_all-Examples" class="tabcontent">

```
#{
  rcpt: [
    action "forward_all" || {
      envelop::add_rcpt("my.address@foo.com");
      envelop::add_rcpt("my.address@bar.com");
      transport::forward_all("127.0.0.1");
    },
    action "forward_all (obj)" || {
      envelop::add_rcpt("my.address@foo2.com");
      envelop::add_rcpt("my.address@bar2.com");
      transport::forward_all(ip4("127.0.0.1"));
    },
  ],
}


```
</div>

</div>
</br>

<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> deliver </h2>

```rust,ignore
fn deliver(rcpt: String) -> ()
fn deliver(rcpt: SharedObject) -> ()
```

<div class="tab">
    <button
    group="deliver"
    id="link-deliver-description"
    class="tablinks active"
    onclick="openTab(event, 'deliver', 'description')">
        Description
    </button>
    <button
    group="deliver"
    id="link-deliver-Args"
    class="tablinks"
    onclick="openTab(event, 'deliver', 'Args')">
        Args
    </button>
    <button
    group="deliver"
    id="link-deliver-Effective smtp stage"
    class="tablinks"
    onclick="openTab(event, 'deliver', 'Effective smtp stage')">
        Effective smtp stage
    </button>
    <button
    group="deliver"
    id="link-deliver-Examples"
    class="tablinks"
    onclick="openTab(event, 'deliver', 'Examples')">
        Examples
    </button></div>

<div group="deliver" id="deliver-description" style="display: block;" markdown="span" class="tabcontent">
Set the delivery method to deliver for a single recipient.
After all rules are evaluated, the email will be sent
to the recipient using the domain of its address.


</div>

<div group="deliver" id="deliver-Args" class="tabcontent">

* `rcpt` - the recipient to apply the method to.


</div>

<div group="deliver" id="deliver-Effective smtp stage" class="tabcontent">

All of them.


</div>

<div group="deliver" id="deliver-Examples" class="tabcontent">

```
#{
  rcpt: [
    action "deliver (str/str)" || {
      envelop::add_rcpt("my.address@foo.com");
      transport::deliver("my.address@foo.com");
    },
    action "deliver (obj/str)" || {
      let rcpt = address("my.address@bar.com");
      envelop::add_rcpt(rcpt);
      transport::deliver(rcpt);
    },
    action "deliver (str/obj)" || {
      let target = ip6("::1");
      envelop::add_rcpt("my.address@baz.com");
      transport::deliver("my.address@baz.com");
    },
    action "deliver (obj/obj)" || {
      let rcpt = address("my.address@boz.com");
      envelop::add_rcpt(rcpt);
      transport::deliver(rcpt);
    },
  ],
}


```
</div>

</div>
</br>

<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> deliver_all </h2>

```rust,ignore
fn deliver_all() -> ()
```

<div class="tab">
    <button
    group="deliver_all"
    id="link-deliver_all-description"
    class="tablinks active"
    onclick="openTab(event, 'deliver_all', 'description')">
        Description
    </button>
    <button
    group="deliver_all"
    id="link-deliver_all-Effective smtp stage"
    class="tablinks"
    onclick="openTab(event, 'deliver_all', 'Effective smtp stage')">
        Effective smtp stage
    </button>
    <button
    group="deliver_all"
    id="link-deliver_all-Examples"
    class="tablinks"
    onclick="openTab(event, 'deliver_all', 'Examples')">
        Examples
    </button></div>

<div group="deliver_all" id="deliver_all-description" style="display: block;" markdown="span" class="tabcontent">
Set the delivery method to deliver for all recipients.
After all rules are evaluated, the email will be sent
to all recipients using the domain of their respective address.


</div>

<div group="deliver_all" id="deliver_all-Effective smtp stage" class="tabcontent">

All of them.


</div>

<div group="deliver_all" id="deliver_all-Examples" class="tabcontent">

```ignore
#{
    delivery: [
       action "setup delivery" || transport::deliver_all(),
    ]
}
```

```
#{
  rcpt: [
    action "deliver_all" || {
      envelop::add_rcpt("my.address@foo.com");
      envelop::add_rcpt("my.address@bar.com");
      transport::deliver_all();
    },
  ],
}

```
</div>

</div>
</br>

<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> mbox </h2>

```rust,ignore
fn mbox(rcpt: String) -> ()
fn mbox(rcpt: SharedObject) -> ()
```

<div class="tab">
    <button
    group="mbox"
    id="link-mbox-description"
    class="tablinks active"
    onclick="openTab(event, 'mbox', 'description')">
        Description
    </button>
    <button
    group="mbox"
    id="link-mbox-Args"
    class="tablinks"
    onclick="openTab(event, 'mbox', 'Args')">
        Args
    </button>
    <button
    group="mbox"
    id="link-mbox-Effective smtp stage"
    class="tablinks"
    onclick="openTab(event, 'mbox', 'Effective smtp stage')">
        Effective smtp stage
    </button>
    <button
    group="mbox"
    id="link-mbox-Examples"
    class="tablinks"
    onclick="openTab(event, 'mbox', 'Examples')">
        Examples
    </button></div>

<div group="mbox" id="mbox-description" style="display: block;" markdown="span" class="tabcontent">
Set the delivery method to mbox for a recipient.
After all rules are evaluated, the email will be stored
locally in the mail box of the recipient if it exists on the server.


</div>

<div group="mbox" id="mbox-Args" class="tabcontent">

* `rcpt` - the recipient to apply the method to.


</div>

<div group="mbox" id="mbox-Effective smtp stage" class="tabcontent">

All of them.


</div>

<div group="mbox" id="mbox-Examples" class="tabcontent">

```ignore
#{
    delivery: [
       action "setup mbox" || transport::mbox("john.doe@example.com"),
    ]
}
```

```
#{
  rcpt: [
    action "setup mbox" || {
        const doe = address("doe@example.com");
        envelop::add_rcpt(doe);
        envelop::add_rcpt("a@example.com");
        transport::mbox(doe);
        transport::mbox("a@example.com");
    },
  ],
}


```
</div>

</div>
</br>

<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> mbox_all </h2>

```rust,ignore
fn mbox_all() -> ()
```

<div class="tab">
    <button
    group="mbox_all"
    id="link-mbox_all-description"
    class="tablinks active"
    onclick="openTab(event, 'mbox_all', 'description')">
        Description
    </button>
    <button
    group="mbox_all"
    id="link-mbox_all-Effective smtp stage"
    class="tablinks"
    onclick="openTab(event, 'mbox_all', 'Effective smtp stage')">
        Effective smtp stage
    </button>
    <button
    group="mbox_all"
    id="link-mbox_all-Examples"
    class="tablinks"
    onclick="openTab(event, 'mbox_all', 'Examples')">
        Examples
    </button></div>

<div group="mbox_all" id="mbox_all-description" style="display: block;" markdown="span" class="tabcontent">
Set the delivery method to mbox for all recipients.
After all rules are evaluated, the email will be stored
locally in the mail box of all recipients if they exists on the server.


</div>

<div group="mbox_all" id="mbox_all-Effective smtp stage" class="tabcontent">

All of them.


</div>

<div group="mbox_all" id="mbox_all-Examples" class="tabcontent">

```ignore
#{
    delivery: [
       action "setup mbox" || transport::mbox_all(),
    ]
}
```

```
#{
  rcpt: [
    action "setup mbox" || {
        const doe = address("doe@example.com");
        envelop::add_rcpt(doe);
        envelop::add_rcpt("a@example.com");
        transport::mbox_all();
    },
  ],
}


```
</div>

</div>
</br>

<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> maildir </h2>

```rust,ignore
fn maildir(rcpt: SharedObject) -> ()
fn maildir(rcpt: String) -> ()
```

<div class="tab">
    <button
    group="maildir"
    id="link-maildir-description"
    class="tablinks active"
    onclick="openTab(event, 'maildir', 'description')">
        Description
    </button>
    <button
    group="maildir"
    id="link-maildir-Args"
    class="tablinks"
    onclick="openTab(event, 'maildir', 'Args')">
        Args
    </button>
    <button
    group="maildir"
    id="link-maildir-Effective smtp stage"
    class="tablinks"
    onclick="openTab(event, 'maildir', 'Effective smtp stage')">
        Effective smtp stage
    </button>
    <button
    group="maildir"
    id="link-maildir-Examples"
    class="tablinks"
    onclick="openTab(event, 'maildir', 'Examples')">
        Examples
    </button></div>

<div group="maildir" id="maildir-description" style="display: block;" markdown="span" class="tabcontent">
Set the delivery method to maildir for a recipient.
After all rules are evaluated, the email will be stored
locally in the `~/Maildir/new/` folder of the recipient's user if it exists on the server.


</div>

<div group="maildir" id="maildir-Args" class="tabcontent">

* `rcpt` - the recipient to apply the method to.


</div>

<div group="maildir" id="maildir-Effective smtp stage" class="tabcontent">

All of them.


</div>

<div group="maildir" id="maildir-Examples" class="tabcontent">
```ignore
#{
    delivery: [
       action "setup maildir" || transport::maildir("john.doe@example.com"),
    ]
}
```

```
#{
  rcpt: [
    action "setup maildir" || {
        const doe = address("doe@example.com");
        envelop::add_rcpt(doe);
        envelop::add_rcpt("a@example.com");
        transport::maildir(doe);
        transport::maildir("a@example.com");
    },
  ],
}


```
</div>

</div>
</br>

<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> maildir_all </h2>

```rust,ignore
fn maildir_all() -> ()
```

<div class="tab">
    <button
    group="maildir_all"
    id="link-maildir_all-description"
    class="tablinks active"
    onclick="openTab(event, 'maildir_all', 'description')">
        Description
    </button>
    <button
    group="maildir_all"
    id="link-maildir_all-Effective smtp stage"
    class="tablinks"
    onclick="openTab(event, 'maildir_all', 'Effective smtp stage')">
        Effective smtp stage
    </button>
    <button
    group="maildir_all"
    id="link-maildir_all-Examples"
    class="tablinks"
    onclick="openTab(event, 'maildir_all', 'Examples')">
        Examples
    </button></div>

<div group="maildir_all" id="maildir_all-description" style="display: block;" markdown="span" class="tabcontent">
Set the delivery method to maildir for all recipients.
After all rules are evaluated, the email will be stored
locally in each `~/Maildir/new` folder of they respective recipient
if they exists on the server.


</div>

<div group="maildir_all" id="maildir_all-Effective smtp stage" class="tabcontent">

All of them.


</div>

<div group="maildir_all" id="maildir_all-Examples" class="tabcontent">

```ignore
#{
    delivery: [
       action "setup maildir" || transport::maildir_all(),
    ]
}
```

```
#{
  rcpt: [
    action "setup maildir" || {
        const doe = address("doe@example.com");
        envelop::add_rcpt(doe);
        envelop::add_rcpt("a@example.com");
        transport::maildir_all();
    },
  ],
}



```
</div>

</div>
</br>
