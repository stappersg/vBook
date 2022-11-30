# global::message



<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn append_header(message: Message, header: String, value: SharedObject) -> ()
```

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn append_header(message: Message, header: String, value: String) -> ()
```

<details>
<summary markdown="span"> details </summary>

Add a header **at the end** of the Header section of the message.

# Examples

```
"X-My-Header: 250 foo\r\n",
"Subject: Unit test are cool\r\n",
"\r\n",
"Hello world!\r\n",

  preq: [
    rule "append_header" || {
      append_header("X-My-Header-2", "bar");
      append_header("X-My-Header-3", identifier("baz"));
    }
  ]
}
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn count_header(message: Message, header: SharedObject) -> int>
```

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn count_header(message: Message, header: String) -> int>
```

<details>
<summary markdown="span"> details </summary>

Count the number of headers with the given name.

# Examples

```
"X-My-Header: foo\r\n",
"X-My-Header: bar\r\n",
"X-My-Header: baz\r\n",
"Subject: Unit test are cool\r\n",
"\r\n",
"Hello world!\r\n",

  preq: [
    rule "count_header" || {
      accept(`250 count is ${count_header("X-My-Header")} and ${count_header(identifier("Subject"))}`);
    }
  ]
}
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn get mail(this: Message) -> String
```

<details>
<summary markdown="span"> details </summary>

Get the message body as a string
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn get_all_headers(message: Message) -> Array>
```

<details>
<summary markdown="span"> details </summary>

Return the complete list of headers.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn get_all_headers(message: Message, name: String) -> Array>
```

<details>
<summary markdown="span"> details </summary>

Return a list of headers bearing the `name` given as argument.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn get_all_headers(message: Message, name: SharedObject) -> Array>
```

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn get_header(message: Message, header: SharedObject) -> String
```

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn get_header(message: Message, header: String) -> String
```

<details>
<summary markdown="span"> details </summary>

return the value of a header if it exists. Otherwise, returns an empty string.

# Examples

```
X-My-Header: 250 foo
Subject: Unit test are cool

Hello world!
; // .eml ends here

  preq: [
    rule "get_header" || {
      if get_header("X-My-Header") != "250 foo"
        || get_header(identifier("Subject")) != "Unit test are cool" {
        deny();
      } else {
        accept(`${get_header("X-My-Header")} ${get_header(identifier("Subject"))}`);
      }
    }
  ]
}
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn get_header_untouched(this: Message, name: String) -> Array>
```

<details>
<summary markdown="span"> details </summary>


</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn has_header(message: Message, header: SharedObject) -> bool
```

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn has_header(message: Message, header: String) -> bool
```

<details>
<summary markdown="span"> details </summary>

Return a boolean, `true` if a header named `header` exists in the message.

# Examples

```
"X-My-Header: foo\r\n",
"Subject: Unit test are cool\r\n",
"\r\n",
"Hello world!\r\n",

  preq: [
    rule "check if header exists" || {
      if has_header("X-My-Header") && has_header(identifier("Subject")) {
        accept();
      } else {
        deny();
      }
    }
  ]
}
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn prepend_header(message: Message, header: String, value: String) -> ()
```

<details>
<summary markdown="span"> details </summary>

Add a header **at the beginning** of the Header section of the message.

# Examples

```
"X-My-Header: 250 foo\r\n",
"Subject: Unit test are cool\r\n",
"\r\n",
"Hello world!\r\n",

  preq: [
    rule "prepend_header" || {
      prepend_header("X-My-Header-2", "bar");
      prepend_header("X-My-Header-3", identifier("baz"));
    }
  ]
}
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn prepend_header(message: Message, header: String, value: SharedObject) -> ()
```

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn remove_header(message: Message, header: String) -> bool
```

<details>
<summary markdown="span"> details </summary>

Remove a header from the raw or parsed email contained in ctx.

# Examples

```
"Subject: The initial header value\r\n",
"\r\n",
"Hello world!\r\n",

  preq: [
    rule "remove_header" || {
      remove_header("Subject");
      if has_header("Subject") { return deny(); }

      prepend_header("Subject-2", "Rust is good");
      remove_header(identifier("Subject-2"));

      prepend_header("Subject-3", "Rust is good !!!!!");

      accept(`250 ${get_header("Subject-3")}`);
    }
  ]
}
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn remove_header(message: Message, header: SharedObject) -> bool
```

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn rename_header(message: Message, old: String, new: String) -> ()
```

<details>
<summary markdown="span"> details </summary>

Change the **key** of a header for a new one.
Do not confuse with [`set_header()`].

# Examples

```
"Subject: The initial header value\r\n",
"\r\n",
"Hello world!\r\n",

  preq: [
    rule "rename_header" || {
      rename_header("Subject", "bob");
      if has_header("Subject") { return deny(); }

      rename_header("bob", identifier("Subject"));
      if has_header("bob") { return deny(); }

      rename_header(identifier("Subject"), "foo");
      if has_header("Subject") { return deny(); }

      rename_header(identifier("foo"), identifier("Subject"));
      if has_header("foo") { return deny(); }

      accept(`250 ${get_header("Subject")}`);
    }
  ]
}
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn rename_header(message: Message, old: SharedObject, new: SharedObject) -> ()
```

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn rename_header(message: Message, old: SharedObject, new: String) -> ()
```

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn rename_header(message: Message, old: String, new: SharedObject) -> ()
```

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn set_header(message: Message, header: String, value: SharedObject) -> ()
```

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn set_header(message: Message, header: String, value: String) -> ()
```

<details>
<summary markdown="span"> details </summary>

Set the **value** of a message header.
Do not confuse with [`rename_header()`].

# Examples

```
"Subject: The initial header value\r\n",
"\r\n",
"Hello world!\r\n",

  preq: [
    rule "set_header" || {
      set_header("Subject", "The header value has been updated");
      set_header("Subject", identifier("The header value has been updated again"));
      accept(`250 ${get_header("Subject")}`);
    }
  ]
}
```
</details>

</div>
</br>

