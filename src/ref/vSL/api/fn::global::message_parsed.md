# global::message_parsed



<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

```rust
fn add_rcpt_message(message: Message, new_addr: SharedObject) -> ()
```

<details>
<summary markdown="span"> details </summary>

Add a recipient to the `To` header of the message.

# Args

* `addr` - the recipient address to add to the `To` header.

# Effective smtp stage

`preq` and onwards.

# Examples

```
#{
    preq: [
       action "update recipients" || add_rcpt_message(address("john.doe@example.com")),
    ]
}
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

```rust
fn add_rcpt_message(message: Message, new_addr: String) -> ()
```

<details>
<summary markdown="span"> details </summary>

Add a recipient to the `To` header of the message.

# Args

* `addr` - the recipient address to add to the `To` header.

# Effective smtp stage

`preq` and onwards.

# Examples

```
#{
    preq: [
       action "update recipients" || add_rcpt_message("john.doe@example.com"),
    ]
}
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

```rust
fn remove_rcpt_message(message: Message, addr: SharedObject) -> ()
```

<details>
<summary markdown="span"> details </summary>

Remove a recipient from the `To` header of the message.

# Args

* `addr` - the recipient to remove to the `To` header.

# Effective smtp stage

`preq` and onwards.

# Examples

```
#{
    preq: [
       action "update recipients" || remove_rcpt_message(address("john.doe@example.com")),
    ]
}
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

```rust
fn remove_rcpt_message(message: Message, addr: String) -> ()
```

<details>
<summary markdown="span"> details </summary>

Remove a recipient from the `To` header of the message.

# Args

* `addr` - the recipient to remove to the `To` header.

# Effective smtp stage

`preq` and onwards.

# Examples

```
#{
    preq: [
       action "update recipients" || remove_rcpt_message("john.doe@example.com"),
    ]
}
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

```rust
fn rewrite_mail_from_message(message: Message, new_addr: String) -> ()
```

<details>
<summary markdown="span"> details </summary>

Change the sender's address in the `From` header of the message.

# Args

* `new_addr` - the new sender address to set.

# Effective smtp stage

`preq` and onwards.

# Examples

```
#{
    preq: [
       action "replace sender" || rewrite_mail_from_message("john.server@example.com"),
    ]
}
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

```rust
fn rewrite_mail_from_message(message: Message, new_addr: SharedObject) -> ()
```

<details>
<summary markdown="span"> details </summary>

Change the sender's address in the `From` header of the message.

# Args

* `new_addr` - the new sender address to set.

# Effective smtp stage

`preq` and onwards.

# Examples

```
#{
    preq: [
       action "replace sender" || rewrite_mail_from_message(address("john.server@example.com")),
    ]
}
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

```rust
fn rewrite_rcpt_message(message: Message, old_addr: String, new_addr: String) -> ()
```

<details>
<summary markdown="span"> details </summary>

Replace a recipient by an other in the `To` header of the message.

# Args

* `old_addr` - the recipient to replace.
* `new_addr` - the new address to use when replacing `old_addr`.

# Effective smtp stage

`preq` and onwards.

# Examples

```
#{
    preq: [
       action "rewrite recipient" || rewrite_rcpt_message("john.doe@example.com", "john-mta@example.com"),
    ]
}
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

```rust
fn rewrite_rcpt_message(message: Message, old_addr: String, new_addr: SharedObject) -> ()
```

<details>
<summary markdown="span"> details </summary>

Replace a recipient by an other in the `To` header of the message.

# Args

* `old_addr` - the recipient to replace.
* `new_addr` - the new address to use when replacing `old_addr`.

# Effective smtp stage

`preq` and onwards.

# Examples

```
#{
    preq: [
       action "rewrite recipient" || rewrite_rcpt_message("john.doe@example.com", address("john-mta@example.com")),
    ]
}
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

```rust
fn rewrite_rcpt_message(message: Message, old_addr: SharedObject, new_addr: SharedObject) -> ()
```

<details>
<summary markdown="span"> details </summary>

Replace a recipient by an other in the `To` header of the message.

# Args

* `old_addr` - the recipient to replace.
* `new_addr` - the new address to use when replacing `old_addr`.

# Effective smtp stage

`preq` and onwards.

# Examples

```
#{
    preq: [
       action "rewrite recipient" || rewrite_rcpt_message(address("john.doe@example.com"), address("john-mta@example.com")),
    ]
}
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

```rust
fn rewrite_rcpt_message(message: Message, old_addr: SharedObject, new_addr: String) -> ()
```

<details>
<summary markdown="span"> details </summary>

Replace a recipient by an other in the `To` header of the message.

# Args

* `old_addr` - the recipient to replace.
* `new_addr` - the new address to use when replacing `old_addr`.

# Effective smtp stage

`preq` and onwards.

# Examples

```
#{
    preq: [
       action "rewrite recipient" || rewrite_rcpt_message(address("john.doe@example.com"), "john-mta@example.com"),
    ]
}
```
</details>

</div>
</br>

