# global::envelop

Functions to inspect and mutate the SMTP envelop.


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> add_rcpt </h2>

```rust,ignore
fn add_rcpt(new_addr: String) -> ()
fn add_rcpt(new_addr: SharedObject) -> ()
```

<details>
<summary markdown="span"> details </summary>

Add a new recipient to the envelop. Note that this does not add
the recipient to the `To` header. Use `msg::add_rcpt` for that.

# Args

* `rcpt` - the new recipient to add.

# Effective smtp stage

All of them.

# Examples

```
#{
    connect: [
       // always deliver a copy of the message to "john.doe@example.com".
       action "rewrite envelop" || envelop::add_rcpt("john.doe@example.com"),
    ]
}
```
</details>

</div>
</br>

<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> bcc </h2>

```rust,ignore
fn bcc(new_addr: SharedObject) -> ()
fn bcc(new_addr: String) -> ()
```

<details>
<summary markdown="span"> details </summary>

Alias for `envelop::add_rcpt`.
</details>

</div>
</br>

<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> rm_rcpt </h2>

```rust,ignore
fn rm_rcpt(addr: SharedObject) -> ()
fn rm_rcpt(addr: String) -> ()
```

<details>
<summary markdown="span"> details </summary>

Remove a recipient from the envelop. Note that this does not remove
the recipient from the `To` header. Use `msg::rm_rcpt` for that.

# Args

* `rcpt` - the recipient to remove.

# Effective smtp stage

All of them.

# Examples

```
#{
    preq: [
       // never deliver to "john.doe@example.com".
       action "rewrite envelop" || envelop::rm_rcpt(address("john.doe@example.com")),
    ]
}
```
</details>

</div>
</br>

<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> rw_mail_from </h2>

```rust,ignore
fn rw_mail_from(new_addr: String) -> ()
fn rw_mail_from(new_addr: SharedObject) -> ()
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
       action "rewrite envelop" || envelop::rw_mail_from("unknown@example.com"),
    ]
}
```
</details>

</div>
</br>

<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> rw_rcpt </h2>

```rust,ignore
fn rw_rcpt(old_addr: String, new_addr: String) -> ()
fn rw_rcpt(old_addr: String, new_addr: SharedObject) -> ()
fn rw_rcpt(old_addr: SharedObject, new_addr: SharedObject) -> ()
fn rw_rcpt(old_addr: SharedObject, new_addr: String) -> ()
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
       action "rewrite envelop" || envelop::rw_rcpt("john.doe@example.com", "john.main@example.com"),
    ]
}
```
</details>

</div>
</br>
