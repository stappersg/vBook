# global::envelop

Functions to inspect and mutate the SMTP envelop.


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> rw_mail_from </h2>

```rust,ignore
fn rw_mail_from(new_addr: SharedObject) -> ()
fn rw_mail_from(new_addr: String) -> ()
```

<div class="tab">
    <button
    group="rw_mail_from"
    id="link-rw_mail_from-description"
    class="tablinks active"
    onclick="openTab(event, 'rw_mail_from', 'description')">
        Description
    </button>
    <button
    group="rw_mail_from"
    id="link-rw_mail_from-Args"
    class="tablinks"
    onclick="openTab(event, 'rw_mail_from', 'Args')">
        Args
    </button>
    <button
    group="rw_mail_from"
    id="link-rw_mail_from-Effective smtp stage"
    class="tablinks"
    onclick="openTab(event, 'rw_mail_from', 'Effective smtp stage')">
        Effective smtp stage
    </button>
    <button
    group="rw_mail_from"
    id="link-rw_mail_from-Examples"
    class="tablinks"
    onclick="openTab(event, 'rw_mail_from', 'Examples')">
        Examples
    </button></div>

<div group="rw_mail_from" id="rw_mail_from-description" style="display: block;" markdown="span" class="tabcontent">
Rewrite the sender received from the `MAIL FROM` command.


</div>

<div group="rw_mail_from" id="rw_mail_from-Args" class="tabcontent">

* `new_addr` - the new string sender address to set.


</div>

<div group="rw_mail_from" id="rw_mail_from-Effective smtp stage" class="tabcontent">

`mail` and onwards.


</div>

<div group="rw_mail_from" id="rw_mail_from-Examples" class="tabcontent">

```
#{
    preq: [
       action "rewrite envelop" || envelop::rw_mail_from("unknown@example.com"),
       // You can use vsl addresses too.
       action "rewrite envelop" || envelop::rw_mail_from(address("john.doe@example.com")),
    ]
}
```
</div>

</div>
</br>

<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> rw_rcpt </h2>

```rust,ignore
fn rw_rcpt(old_addr: SharedObject, new_addr: String) -> ()
fn rw_rcpt(old_addr: String, new_addr: String) -> ()
fn rw_rcpt(old_addr: SharedObject, new_addr: SharedObject) -> ()
fn rw_rcpt(old_addr: String, new_addr: SharedObject) -> ()
```

<div class="tab">
    <button
    group="rw_rcpt"
    id="link-rw_rcpt-description"
    class="tablinks active"
    onclick="openTab(event, 'rw_rcpt', 'description')">
        Description
    </button>
    <button
    group="rw_rcpt"
    id="link-rw_rcpt-Args"
    class="tablinks"
    onclick="openTab(event, 'rw_rcpt', 'Args')">
        Args
    </button>
    <button
    group="rw_rcpt"
    id="link-rw_rcpt-Effective smtp stage"
    class="tablinks"
    onclick="openTab(event, 'rw_rcpt', 'Effective smtp stage')">
        Effective smtp stage
    </button>
    <button
    group="rw_rcpt"
    id="link-rw_rcpt-Examples"
    class="tablinks"
    onclick="openTab(event, 'rw_rcpt', 'Examples')">
        Examples
    </button></div>

<div group="rw_rcpt" id="rw_rcpt-description" style="display: block;" markdown="span" class="tabcontent">
Replace a recipient received by a `RCPT TO` command.


</div>

<div group="rw_rcpt" id="rw_rcpt-Args" class="tabcontent">

* `old_addr` - the recipient to replace.
* `new_addr` - the new address to use when replacing `old_addr`.


</div>

<div group="rw_rcpt" id="rw_rcpt-Effective smtp stage" class="tabcontent">

`rcpt` and onwards.


</div>

<div group="rw_rcpt" id="rw_rcpt-Examples" class="tabcontent">

```
#{
    preq: [
       // You can use strings or addresses as parameters.
       action "rewrite envelop" || envelop::rw_rcpt("john.doe@example.com", "john.main@example.com"),
       action "rewrite envelop" || envelop::rw_rcpt(address("john.doe@example.com"), "john.main@example.com"),
       action "rewrite envelop" || envelop::rw_rcpt("john.doe@example.com", address("john.main@example.com")),
       action "rewrite envelop" || envelop::rw_rcpt(address("john.doe@example.com"), address("john.main@example.com")),
    ]
}
```
</div>

</div>
</br>

<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> add_rcpt </h2>

```rust,ignore
fn add_rcpt(new_addr: SharedObject) -> ()
fn add_rcpt(new_addr: String) -> ()
```

<div class="tab">
    <button
    group="add_rcpt"
    id="link-add_rcpt-description"
    class="tablinks active"
    onclick="openTab(event, 'add_rcpt', 'description')">
        Description
    </button>
    <button
    group="add_rcpt"
    id="link-add_rcpt-Args"
    class="tablinks"
    onclick="openTab(event, 'add_rcpt', 'Args')">
        Args
    </button>
    <button
    group="add_rcpt"
    id="link-add_rcpt-Effective smtp stage"
    class="tablinks"
    onclick="openTab(event, 'add_rcpt', 'Effective smtp stage')">
        Effective smtp stage
    </button>
    <button
    group="add_rcpt"
    id="link-add_rcpt-Examples"
    class="tablinks"
    onclick="openTab(event, 'add_rcpt', 'Examples')">
        Examples
    </button></div>

<div group="add_rcpt" id="add_rcpt-description" style="display: block;" markdown="span" class="tabcontent">
Add a new recipient to the envelop. Note that this does not add
the recipient to the `To` header. Use `msg::add_rcpt` for that.


</div>

<div group="add_rcpt" id="add_rcpt-Args" class="tabcontent">

* `rcpt` - the new recipient to add.


</div>

<div group="add_rcpt" id="add_rcpt-Effective smtp stage" class="tabcontent">

All of them.


</div>

<div group="add_rcpt" id="add_rcpt-Examples" class="tabcontent">

```
#{
    connect: [
       // always deliver a copy of the message to "john.doe@example.com".
       action "rewrite envelop" || envelop::add_rcpt("john.doe@example.com"),
       action "rewrite envelop" || envelop::add_rcpt(address("john.doe@example.com")),
    ]
}
```
</div>

</div>
</br>

<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> bcc </h2>

```rust,ignore
fn bcc(new_addr: String) -> ()
fn bcc(new_addr: SharedObject) -> ()
```

<div class="tab">
    <button
    group="bcc"
    id="link-bcc-description"
    class="tablinks active"
    onclick="openTab(event, 'bcc', 'description')">
        Description
    </button></div>

<div group="bcc" id="bcc-description" style="display: block;" markdown="span" class="tabcontent">
Alias for `envelop::add_rcpt`.
</div>

</div>
</br>

<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> rm_rcpt </h2>

```rust,ignore
fn rm_rcpt(addr: SharedObject) -> ()
fn rm_rcpt(addr: String) -> ()
```

<div class="tab">
    <button
    group="rm_rcpt"
    id="link-rm_rcpt-description"
    class="tablinks active"
    onclick="openTab(event, 'rm_rcpt', 'description')">
        Description
    </button>
    <button
    group="rm_rcpt"
    id="link-rm_rcpt-Args"
    class="tablinks"
    onclick="openTab(event, 'rm_rcpt', 'Args')">
        Args
    </button>
    <button
    group="rm_rcpt"
    id="link-rm_rcpt-Effective smtp stage"
    class="tablinks"
    onclick="openTab(event, 'rm_rcpt', 'Effective smtp stage')">
        Effective smtp stage
    </button>
    <button
    group="rm_rcpt"
    id="link-rm_rcpt-Examples"
    class="tablinks"
    onclick="openTab(event, 'rm_rcpt', 'Examples')">
        Examples
    </button></div>

<div group="rm_rcpt" id="rm_rcpt-description" style="display: block;" markdown="span" class="tabcontent">
Remove a recipient from the envelop. Note that this does not remove
the recipient from the `To` header. Use `msg::rm_rcpt` for that.


</div>

<div group="rm_rcpt" id="rm_rcpt-Args" class="tabcontent">

* `rcpt` - the recipient to remove.


</div>

<div group="rm_rcpt" id="rm_rcpt-Effective smtp stage" class="tabcontent">

All of them.


</div>

<div group="rm_rcpt" id="rm_rcpt-Examples" class="tabcontent">

```
#{
    preq: [
       // never deliver to "john.doe@example.com".
       action "rewrite envelop" || envelop::rm_rcpt("john.doe@example.com"),
       action "rewrite envelop" || envelop::rm_rcpt(address("john.doe@example.com")),
    ]
}
```
</div>

</div>
</br>
