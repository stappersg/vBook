# global::message



<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

```rust
fn append_header(message: Message, header: String, value: SharedObject) -> ()
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
#{
    postq: [
        action "append a header" || {
            append_header("X-JOHN", "received by john's server.");
        }
    ],
}
```

```
"X-My-Header: 250 foo\r\n",
"Subject: Unit test are cool\r\n",
"\r\n",
"Hello world!\r\n",

#{
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


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

```rust
fn append_header(message: Message, header: String, value: String) -> ()
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
#{
    postq: [
        action "append a header" || {
            append_header("X-JOHN", "received by john's server.");
        }
    ],
}
```

```
"X-My-Header: 250 foo\r\n",
"Subject: Unit test are cool\r\n",
"\r\n",
"Hello world!\r\n",

#{
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


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

```rust
fn count_header(message: Message, header: String) -> int
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
#{
    postq: [
        action "display VSMTP header" || {
            print(get_header("X-VSMTP"));
        }
    ],
}
```

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
      accept(`250 count is ${count_header("X-My-Header")} and ${count_header(identifier("Subject"))}`);
    }
  ]
}
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

```rust
fn count_header(message: Message, header: SharedObject) -> int
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
#{
    postq: [
        action "display VSMTP header" || {
            print(get_header(identifier("X-VSMTP")));
        }
    ],
}
```

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
      accept(`250 count is ${count_header("X-My-Header")} and ${count_header(identifier("Subject"))}`);
    }
  ]
}
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

```rust
fn get mail(this: Message) -> String
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
       action "display email content" || log("trace", `email content: ${mail()}`),
    ]
}
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

```rust
fn get_all_headers(message: Message) -> Array
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
#{
    postq: [
        action "log display headers" || {
            log("trace", `${get_all_headers()}`);
        }
    ],
}
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

```rust
fn get_all_headers(message: Message, name: SharedObject) -> Array
```

<details>
<summary markdown="span"> details </summary>

Get a list of all values of a specific header from the incoming message.

# Args

* `header` - the name of the header to search.

# Return

* `array` - all header values, or an empty array if the header was not found.

# Effective smtp stage

All of them, although it is most useful in the `preq` stage because this
is when the email body is received.

# Examples

```
#{
    postq: [
        action "display return path" || {
            print(get_all_headers(identifier("Return-Path")));
        }
    ],
}
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

```rust
fn get_all_headers(message: Message, name: String) -> Array
```

<details>
<summary markdown="span"> details </summary>

Get a list of all values of a specific header from the incoming message.

# Args

* `header` - the name of the header to search.

# Return

* `array` - all header values, or an empty array if the header was not found.

# Effective smtp stage

All of them, although it is most useful in the `preq` stage because this
is when the email body is received.

# Examples

```
#{
    postq: [
        action "display return path" || {
            print(get_all_headers("Return-Path"));
        }
    ],
}
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

```rust
fn get_header(message: Message, header: String) -> String
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
#{
    postq: [
        action "display VSMTP header" || {
            print(get_header("X-VSMTP"));
        }
    ],
}
```

```
X-My-Header: 250 foo
Subject: Unit test are cool

Hello world!
; // .eml ends here

#{
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


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

```rust
fn get_header(message: Message, header: SharedObject) -> String
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
#{
    postq: [
        action "display VSMTP header" || {
            print(get_header(identifier("X-VSMTP")));
        }
    ],
}
```

```
X-My-Header: 250 foo
Subject: Unit test are cool

Hello world!
; // .eml ends here

#{
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


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

```rust
fn get_header_untouched(this: Message, name: String) -> Array
```

<details>
<summary markdown="span"> details </summary>


</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

```rust
fn has_header(message: Message, header: SharedObject) -> bool
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
#{
    postq: [
        action "check for VSMTP header" || {
            if has_header(identifier("X-VSMTP")) {
                log("info", "incoming message could be from another vsmtp server");
            }
        }
    ],
}
```

```
// Message example.
"X-My-Header: foo\r\n",
"Subject: Unit test are cool\r\n",
"\r\n",
"Hello world!\r\n",

#{
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


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

```rust
fn has_header(message: Message, header: String) -> bool
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
#{
    postq: [
        action "check for VSMTP header" || {
            if has_header("X-VSMTP") {
                log("info", "incoming message could be from another vsmtp server");
            }
        }
    ],
}
```

```
// Message example.
"X-My-Header: foo\r\n",
"Subject: Unit test are cool\r\n",
"\r\n",
"Hello world!\r\n",

#{
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


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

```rust
fn prepend_header(message: Message, header: String, value: String) -> ()
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
#{
    postq: [
        action "prepend a header" || {
            prepend_header("X-JOHN", "received by john's server.");
        }
    ],
}
```

```
"X-My-Header: 250 foo\r\n",
"Subject: Unit test are cool\r\n",
"\r\n",
"Hello world!\r\n",

#{
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


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

```rust
fn prepend_header(message: Message, header: String, value: SharedObject) -> ()
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
#{
    postq: [
        action "prepend a header" || {
            prepend_header("X-JOHN", "received by john's server.");
        }
    ],
}
```

```
"X-My-Header: 250 foo\r\n",
"Subject: Unit test are cool\r\n",
"\r\n",
"Hello world!\r\n",

#{
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


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

```rust
fn remove_header(message: Message, header: String) -> bool
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
#{
    postq: [
        action "remove one X-VSMTP header" || {
            remove_header("X-VSMTP");
        },

        // There can be multiple headers with the same name.
        // Since `remove_header` return `true` when it removes an
        // header, you can use a `while` loop to remove all headers
        // that bear the same name.
        action "remove all X-VSMTP headers" || {
            while remove_header("X-VSMTP") is true {}
        },
    ],
}
```

```
"Subject: The initial header value\r\n",
"\r\n",
"Hello world!\r\n",

#{
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


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

```rust
fn remove_header(message: Message, header: SharedObject) -> bool
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
#{
    postq: [
        action "remove one X-VSMTP header" || {
            remove_header("X-VSMTP");
        },

        // There can be multiple headers with the same name.
        // Since `remove_header` return `true` when it removes an
        // header, you can use a `while` loop to remove all headers
        // that bear the same name.
        action "remove all X-VSMTP headers" || {
            while remove_header("X-VSMTP") is true {}
        },
    ],
}
```

```
"Subject: The initial header value\r\n",
"\r\n",
"Hello world!\r\n",

#{
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


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

```rust
fn rename_header(message: Message, old: SharedObject, new: String) -> ()
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
#{
    postq: [
        action "rename header" || {
            rename_header("X-To-Rename", "X-Renamed");
        }
    ],
}
```

```
"Subject: The initial header value\r\n",
"\r\n",
"Hello world!\r\n",

#{
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


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

```rust
fn rename_header(message: Message, old: String, new: String) -> ()
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
#{
    postq: [
        action "rename header" || {
            rename_header("X-To-Rename", "X-Renamed");
        }
    ],
}
```

```
"Subject: The initial header value\r\n",
"\r\n",
"Hello world!\r\n",

#{
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


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

```rust
fn rename_header(message: Message, old: String, new: SharedObject) -> ()
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
#{
    postq: [
        action "rename header" || {
            rename_header("X-To-Rename", "X-Renamed");
        }
    ],
}
```

```
"Subject: The initial header value\r\n",
"\r\n",
"Hello world!\r\n",

#{
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


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

```rust
fn rename_header(message: Message, old: SharedObject, new: SharedObject) -> ()
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
#{
    postq: [
        action "rename header" || {
            rename_header("X-To-Rename", "X-Renamed");
        }
    ],
}
```

```
"Subject: The initial header value\r\n",
"\r\n",
"Hello world!\r\n",

#{
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


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

```rust
fn set_header(message: Message, header: String, value: SharedObject) -> ()
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
#{
    postq: [
        action "update subject" || {
            let subject = get_header("Subject");
            set_header("Subject", `${subject} (analyzed by vsmtp)`);
        }
    ],
}
```

```
"Subject: The initial header value\r\n",
"\r\n",
"Hello world!\r\n",

#{
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


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

```rust
fn set_header(message: Message, header: String, value: String) -> ()
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
#{
    postq: [
        action "update subject" || {
            let subject = get_header("Subject");
            set_header("Subject", `${subject} (analyzed by vsmtp)`);
        }
    ],
}
```

```
"Subject: The initial header value\r\n",
"\r\n",
"Hello world!\r\n",

#{
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

