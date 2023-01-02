# global::msg

Inspect incoming messages.



<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> add_rcpt </h2>

```rust,ignore
fn add_rcpt(new_addr: String) -> ()
fn add_rcpt(new_addr: SharedObject) -> ()
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
       action "update recipients" || msg::add_rcpt("john.doe@example.com"),
    ]
}
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> append_header </h2>

```rust,ignore
fn append_header(header: String, value: String) -> ()
fn append_header(header: String, value: SharedObject) -> ()
```

<details>
<summary markdown="span"> details </summary>

Add a new header **at the end** of the header list in the message.

# Args

* `header` - the name of the header to append.
* `value` - the value of the header to append.

# Effective smtp stage

All of them. Even though the email is not received at the current stage,
vsmtp stores new headers and will add them on top of the ones received once
the `preq` stage is reached.

# Examples

```
"X-My-Header: 250 foo\r\n",
"Subject: Unit test are cool\r\n",
"\r\n",
"Hello world!\r\n",

#{
  preq: [
    rule "append_header" || {
      msg::append_header("X-My-Header-2", "bar");
      msg::append_header("X-My-Header-3", identifier("baz"));
    }
  ]
}
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> count_header </h2>

```rust,ignore
fn count_header(header: SharedObject) -> int
fn count_header(header: String) -> int
```

<details>
<summary markdown="span"> details </summary>

Count the number of headers with the given name.

# Args

* `header` - the name of the header to count.

# Return

* `number` - the number headers with the same name.

# Effective smtp stage

All of them, although it is most useful in the `preq` stage because this
is when the email body is received.

# Examples

```
"X-My-Header: foo\r\n",
"X-My-Header: bar\r\n",
"X-My-Header: baz\r\n",
"Subject: Unit test are cool\r\n",
"\r\n",
"Hello world!\r\n",

#{
  preq: [
    rule "count_header" || {
      state::accept(`250 count is ${msg::count_header("X-My-Header")} and ${msg::count_header(identifier("Subject"))}`);
    }
  ]
}
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> get_all_headers </h2>

```rust,ignore
fn get_all_headers() -> Array
fn get_all_headers(name: SharedObject) -> Array
fn get_all_headers(name: String) -> Array
```

<details>
<summary markdown="span"> details </summary>

Get a list of all headers.

# Return

* `array` - all of the headers found in the message.

# Effective smtp stage

All of them, although it is most useful in the `preq` stage because this
is when the email body is received.

# Examples

```
X-My-Header: 250 foo
Subject: Unit test are cool

Hello world!
; // .eml ends here

#{
  preq: [
    rule "display headers" || {
        log("info", `header: ${get_all_headers}`);
    }
  ]
}
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> get_header </h2>

```rust,ignore
fn get_header(header: SharedObject) -> String
fn get_header(header: String) -> String
```

<details>
<summary markdown="span"> details </summary>

Get a specific header from the incoming message.

# Args

* `header` - the name of the header to get.

# Return

* `string` - the header value, or an empty string if the header was not found.

# Effective smtp stage

All of them, although it is most useful in the `preq` stage because this
is when the email body is received.

# Examples

```
X-My-Header: 250 foo
Subject: Unit test are cool

Hello world!
; // .eml ends here

#{
  preq: [
    rule "get_header" || {
      if msg::get_header("X-My-Header") != "250 foo"
        || msg::get_header(identifier("Subject")) != "Unit test are cool" {
        state::deny();
      } else {
        state::accept(`${msg::get_header("X-My-Header")} ${msg::get_header(identifier("Subject"))}`);
      }
    }
  ]
}
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> get_header_untouched </h2>

```rust,ignore
fn get_header_untouched(name: String) -> Array
```

<details>
<summary markdown="span"> details </summary>

Get a list of all headers of a specific name with it's name and value
separated by a column.

# Args

* `header` - the name of the header to search.

# Return

* `array` - all header values, or an empty array if the header was not found.

# Effective smtp stage

All of them, although it is most useful in the `preq` stage because this
is when the email body is received.

# Examples

```
X-My-Header: 250 foo
Subject: Unit test are cool

Hello world!
; // .eml ends here

#{
    postq: [
        action "display return path" || {
            // Will display "Return-Path: value".
            log("info", msg::get_header_untouched("Return-Path"));
        }
    ],
}
```    
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> has_header </h2>

```rust,ignore
fn has_header(header: SharedObject) -> bool
fn has_header(header: String) -> bool
```

<details>
<summary markdown="span"> details </summary>

Checks if the message contains a specific header.

# Args

* `header` - the name of the header to search.

# Effective smtp stage

All of them, although it is most useful in the `preq` stage because the
email is received at this point.

# Examples

```
// Message example.
"X-My-Header: foo\r\n",
"Subject: Unit test are cool\r\n",
"\r\n",
"Hello world!\r\n",

#{
  preq: [
    rule "check if header exists" || {
      if msg::has_header("X-My-Header") && msg::has_header(identifier("Subject")) {
        state::accept();
      } else {
        state::deny();
      }
    }
  ]
}
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> mail </h2>

```rust,ignore
fn mail() -> String
```

<details>
<summary markdown="span"> details </summary>

Get a copy of the whole email as a string.

# Effective smtp stage

`preq` and onwards.

# Example

```
#{
    postq: [
       action "display email content" || log("trace", `email content: ${msg::mail()}`),
    ]
}
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> prepend_header </h2>

```rust,ignore
fn prepend_header(header: String, value: SharedObject) -> ()
fn prepend_header(header: String, value: String) -> ()
```

<details>
<summary markdown="span"> details </summary>

Add a new header on top all other headers in the message.

# Args

* `header` - the name of the header to prepend.
* `value` - the value of the header to prepend.

# Effective smtp stage

All of them. Even though the email is not received at the current stage,
vsmtp stores new headers and will add them on top of the ones received once
the `preq` stage is reached.

# Examples

```
"X-My-Header: 250 foo\r\n",
"Subject: Unit test are cool\r\n",
"\r\n",
"Hello world!\r\n",

#{
  preq: [
    rule "prepend_header" || {
      msg::prepend_header("X-My-Header-2", "bar");
      msg::prepend_header("X-My-Header-3", identifier("baz"));
    }
  ]
}
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> rename_header </h2>

```rust,ignore
fn rename_header(old: String, new: String) -> ()
fn rename_header(old: String, new: SharedObject) -> ()
fn rename_header(old: SharedObject, new: String) -> ()
fn rename_header(old: SharedObject, new: SharedObject) -> ()
```

<details>
<summary markdown="span"> details </summary>

Replace an existing header name by a new value.

# Args

* `old` - the name of the header to rename.
* `new` - the new new of the header.

# Effective smtp stage

All of them, although it is most useful in the `preq` stage because this
is when the email body is received.

# Examples

```
"Subject: The initial header value\r\n",
"\r\n",
"Hello world!\r\n",

#{
  preq: [
    rule "rename_header" || {
      msg::rename_header("Subject", "bob");
      if msg::has_header("Subject") { return state::deny(); }

      msg::rename_header("bob", identifier("Subject"));
      if msg::has_header("bob") { return state::deny(); }

      msg::rename_header(identifier("Subject"), "foo");
      if msg::has_header("Subject") { return state::deny(); }

      msg::rename_header(identifier("foo"), identifier("Subject"));
      if msg::has_header("foo") { return state::deny(); }

      state::accept(`250 ${msg::get_header("Subject")}`);
    }
  ]
}
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> rm_header </h2>

```rust,ignore
fn rm_header(header: String) -> bool
fn rm_header(header: SharedObject) -> bool
```

<details>
<summary markdown="span"> details </summary>

Remove an existing header from the message.

# Args

* `header` - the name of the header to remove.

# Return

* a boolean value, true if a header has been removed, false otherwise.

# Effective smtp stage

All of them, although it is most useful in the `preq` stage because this
is when the email body is received.

# Examples

```
"Subject: The initial header value\r\n",
"\r\n",
"Hello world!\r\n",

#{
  preq: [
    rule "remove_header" || {
      msg::rm_header("Subject");
      if msg::has_header("Subject") { return state::deny(); }

      msg::prepend_header("Subject-2", "Rust is good");
      msg::rm_header(identifier("Subject-2"));

      msg::prepend_header("Subject-3", "Rust is good !!!!!");

      state::accept(`250 ${msg::get_header("Subject-3")}`);
    }
  ]
}
```
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

Remove a recipient from the `To` header of the message.

# Args

* `addr` - the recipient to remove to the `To` header.

# Effective smtp stage

`preq` and onwards.

# Examples

```
#{
    preq: [
       action "update recipients" || msg::rm_rcpt(address("john.doe@example.com")),
    ]
}
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> rw_mail_from </h2>

```rust,ignore
fn rw_mail_from(new_addr: SharedObject) -> ()
fn rw_mail_from(new_addr: String) -> ()
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
       action "replace sender" || msg::rw_mail_from(address("john.server@example.com")),
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
fn rw_rcpt(old_addr: SharedObject, new_addr: String) -> ()
fn rw_rcpt(old_addr: String, new_addr: SharedObject) -> ()
fn rw_rcpt(old_addr: SharedObject, new_addr: SharedObject) -> ()
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
       action "rewrite recipient" || msg::rw_rcpt("john.doe@example.com", "john-mta@example.com"),
    ]
}
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> set_header </h2>

```rust,ignore
fn set_header(header: String, value: SharedObject) -> ()
fn set_header(header: String, value: String) -> ()
```

<details>
<summary markdown="span"> details </summary>

Replace an existing header value by a new value, or append a new header
to the message.

# Args

* `header` - the name of the header to set or add.
* `value` - the value of the header to set or add.

# Effective smtp stage

All of them. Even though the email is not received at the current stage,
vsmtp stores new headers and will add them on top to the ones received once
the `preq` stage is reached.

Be aware that if you want to set a header value from the original message,
you must use `set_header` in the `preq` stage and onwards.

# Examples

```
"Subject: The initial header value\r\n",
"\r\n",
"Hello world!\r\n",

#{
  preq: [
    rule "set_header" || {
      msg::set_header("Subject", "The header value has been updated");
      msg::set_header("Subject", identifier("The header value has been updated again"));
      state::accept(`250 ${msg::get_header("Subject")}`);
    }
  ]
}
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> to_string </h2>

```rust,ignore
fn to_string(message: Message) -> String
```

<details>
<summary markdown="span"> details </summary>

Generate the `.eml` representation of the message.
</details>

</div>
</br>

