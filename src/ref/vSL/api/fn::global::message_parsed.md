# global::message_parsed



<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn add_rcpt_message(message: Message, new_addr: SharedObject) -> ()
```

<details>
<summary markdown="span"> details </summary>

add a recipient to the 'To' mail header.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn add_rcpt_message(message: Message, new_addr: String) -> ()
```

<details>
<summary markdown="span"> details </summary>

add a recipient to the 'To' mail header.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn remove_rcpt_message(message: Message, addr: String) -> ()
```

<details>
<summary markdown="span"> details </summary>

remove a recipient from the mail 'To' header.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn remove_rcpt_message(message: Message, addr: SharedObject) -> ()
```

<details>
<summary markdown="span"> details </summary>

remove a recipient from the mail 'To' header.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn rewrite_mail_from_message(message: Message, new_addr: String) -> ()
```

<details>
<summary markdown="span"> details </summary>

replace the value of the `From` header by another address.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn rewrite_mail_from_message(message: Message, new_addr: SharedObject) -> ()
```

<details>
<summary markdown="span"> details </summary>

replace the value of the `From` header by another address.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn rewrite_rcpt_message(message: Message, old_addr: String, new_addr: SharedObject) -> ()
```

<details>
<summary markdown="span"> details </summary>

replace the value of the `To:` header by another address.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn rewrite_rcpt_message(message: Message, old_addr: SharedObject, new_addr: String) -> ()
```

<details>
<summary markdown="span"> details </summary>

replace the value of the `To:` header by another address.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn rewrite_rcpt_message(message: Message, old_addr: String, new_addr: String) -> ()
```

<details>
<summary markdown="span"> details </summary>

replace the value of the `To:` header by another address.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn rewrite_rcpt_message(message: Message, old_addr: SharedObject, new_addr: SharedObject) -> ()
```

<details>
<summary markdown="span"> details </summary>

replace the value of the `To:` header by another address.
</details>

</div>
</br>

