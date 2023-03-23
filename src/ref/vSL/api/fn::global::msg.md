# global::msg

Inspect incoming messages.


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> to_string </h2>

```rust,ignore
fn to_string(message: Message) -> String
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
Generate the `.eml` representation of the message.
</div>

</div>
</br>

<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> has_header </h2>

```rust,ignore
fn has_header(header: SharedObject) -> bool
fn has_header(header: String) -> bool
```

<div class="tab">
    <button
    group="has_header"
    id="link-has_header-description"
    class="tablinks active"
    onclick="openTab(event, 'has_header', 'description')">
        Description
    </button>
    <button
    group="has_header"
    id="link-has_header-Args"
    class="tablinks"
    onclick="openTab(event, 'has_header', 'Args')">
        Args
    </button>
    <button
    group="has_header"
    id="link-has_header-Effective smtp stage"
    class="tablinks"
    onclick="openTab(event, 'has_header', 'Effective smtp stage')">
        Effective smtp stage
    </button>
    <button
    group="has_header"
    id="link-has_header-Examples"
    class="tablinks"
    onclick="openTab(event, 'has_header', 'Examples')">
        Examples
    </button></div>

<div group="has_header" id="has_header-description" style="display: block;" markdown="span" class="tabcontent">
Checks if the message contains a specific header.


</div>

<div group="has_header" id="has_header-Args" class="tabcontent">

* `header` - the name of the header to search.


</div>

<div group="has_header" id="has_header-Effective smtp stage" class="tabcontent">

All of them, although it is most useful in the `preq` stage because the
email is received at this point.


</div>

<div group="has_header" id="has_header-Examples" class="tabcontent">

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
</div>

</div>
</br>

<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> count_header </h2>

```rust,ignore
fn count_header(header: String) -> int
fn count_header(header: SharedObject) -> int
```

<div class="tab">
    <button
    group="count_header"
    id="link-count_header-description"
    class="tablinks active"
    onclick="openTab(event, 'count_header', 'description')">
        Description
    </button>
    <button
    group="count_header"
    id="link-count_header-Args"
    class="tablinks"
    onclick="openTab(event, 'count_header', 'Args')">
        Args
    </button>
    <button
    group="count_header"
    id="link-count_header-Return"
    class="tablinks"
    onclick="openTab(event, 'count_header', 'Return')">
        Return
    </button>
    <button
    group="count_header"
    id="link-count_header-Effective smtp stage"
    class="tablinks"
    onclick="openTab(event, 'count_header', 'Effective smtp stage')">
        Effective smtp stage
    </button>
    <button
    group="count_header"
    id="link-count_header-Examples"
    class="tablinks"
    onclick="openTab(event, 'count_header', 'Examples')">
        Examples
    </button></div>

<div group="count_header" id="count_header-description" style="display: block;" markdown="span" class="tabcontent">
Count the number of headers with the given name.


</div>

<div group="count_header" id="count_header-Args" class="tabcontent">

* `header` - the name of the header to count.


</div>

<div group="count_header" id="count_header-Return" class="tabcontent">

* `number` - the number headers with the same name.


</div>

<div group="count_header" id="count_header-Effective smtp stage" class="tabcontent">

All of them, although it is most useful in the `preq` stage because this
is when the email body is received.


</div>

<div group="count_header" id="count_header-Examples" class="tabcontent">

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
</div>

</div>
</br>

<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> get_header </h2>

```rust,ignore
fn get_header(header: SharedObject) -> String
fn get_header(header: String) -> String
```

<div class="tab">
    <button
    group="get_header"
    id="link-get_header-description"
    class="tablinks active"
    onclick="openTab(event, 'get_header', 'description')">
        Description
    </button>
    <button
    group="get_header"
    id="link-get_header-Args"
    class="tablinks"
    onclick="openTab(event, 'get_header', 'Args')">
        Args
    </button>
    <button
    group="get_header"
    id="link-get_header-Return"
    class="tablinks"
    onclick="openTab(event, 'get_header', 'Return')">
        Return
    </button>
    <button
    group="get_header"
    id="link-get_header-Effective smtp stage"
    class="tablinks"
    onclick="openTab(event, 'get_header', 'Effective smtp stage')">
        Effective smtp stage
    </button>
    <button
    group="get_header"
    id="link-get_header-Examples"
    class="tablinks"
    onclick="openTab(event, 'get_header', 'Examples')">
        Examples
    </button></div>

<div group="get_header" id="get_header-description" style="display: block;" markdown="span" class="tabcontent">
Get a specific header from the incoming message.


</div>

<div group="get_header" id="get_header-Args" class="tabcontent">

* `header` - the name of the header to get.


</div>

<div group="get_header" id="get_header-Return" class="tabcontent">

* `string` - the header value, or an empty string if the header was not found.


</div>

<div group="get_header" id="get_header-Effective smtp stage" class="tabcontent">

All of them, although it is most useful in the `preq` stage because this
is when the email body is received.


</div>

<div group="get_header" id="get_header-Examples" class="tabcontent">

```
X-My-Header: 250 foo
Subject: Unit test are cool

Hello world!
; // .eml ends here

let rules = r#"
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
</div>

</div>
</br>

<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> get_all_headers </h2>

```rust,ignore
fn get_all_headers() -> Array
fn get_all_headers(name: String) -> Array
fn get_all_headers(name: SharedObject) -> Array
```

<div class="tab">
    <button
    group="get_all_headers"
    id="link-get_all_headers-description"
    class="tablinks active"
    onclick="openTab(event, 'get_all_headers', 'description')">
        Description
    </button>
    <button
    group="get_all_headers"
    id="link-get_all_headers-Args"
    class="tablinks"
    onclick="openTab(event, 'get_all_headers', 'Args')">
        Args
    </button>
    <button
    group="get_all_headers"
    id="link-get_all_headers-Return"
    class="tablinks"
    onclick="openTab(event, 'get_all_headers', 'Return')">
        Return
    </button>
    <button
    group="get_all_headers"
    id="link-get_all_headers-Effective smtp stage"
    class="tablinks"
    onclick="openTab(event, 'get_all_headers', 'Effective smtp stage')">
        Effective smtp stage
    </button>
    <button
    group="get_all_headers"
    id="link-get_all_headers-Examples"
    class="tablinks"
    onclick="openTab(event, 'get_all_headers', 'Examples')">
        Examples
    </button></div>

<div group="get_all_headers" id="get_all_headers-description" style="display: block;" markdown="span" class="tabcontent">
Get a list of all headers.


</div>

<div group="get_all_headers" id="get_all_headers-Args" class="tabcontent">

* `header` - the name of the header to search. (optional, if not set, returns every header)


</div>

<div group="get_all_headers" id="get_all_headers-Return" class="tabcontent">

* `array` - all of the headers found in the message.


</div>

<div group="get_all_headers" id="get_all_headers-Effective smtp stage" class="tabcontent">

All of them, although it is most useful in the `preq` stage because this
is when the email body is received.


</div>

<div group="get_all_headers" id="get_all_headers-Examples" class="tabcontent">

```
X-My-Header: 250 foo
Subject: Unit test are cool

Hello world!
; // .eml ends here

#{
  preq: [
    rule "display headers" || {
        log("info", `all headers: ${msg::get_all_headers()}`);
        log("info", `all "Return-Path" headers: ${msg::get_all_headers("Return-Path")}`);
    }
  ]
}
```
</div>

</div>
</br>

<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> get_header_untouched </h2>

```rust,ignore
fn get_header_untouched(name: String) -> Array
```

<div class="tab">
    <button
    group="get_header_untouched"
    id="link-get_header_untouched-description"
    class="tablinks active"
    onclick="openTab(event, 'get_header_untouched', 'description')">
        Description
    </button>
    <button
    group="get_header_untouched"
    id="link-get_header_untouched-Args"
    class="tablinks"
    onclick="openTab(event, 'get_header_untouched', 'Args')">
        Args
    </button>
    <button
    group="get_header_untouched"
    id="link-get_header_untouched-Return"
    class="tablinks"
    onclick="openTab(event, 'get_header_untouched', 'Return')">
        Return
    </button>
    <button
    group="get_header_untouched"
    id="link-get_header_untouched-Effective smtp stage"
    class="tablinks"
    onclick="openTab(event, 'get_header_untouched', 'Effective smtp stage')">
        Effective smtp stage
    </button>
    <button
    group="get_header_untouched"
    id="link-get_header_untouched-Examples"
    class="tablinks"
    onclick="openTab(event, 'get_header_untouched', 'Examples')">
        Examples
    </button></div>

<div group="get_header_untouched" id="get_header_untouched-description" style="display: block;" markdown="span" class="tabcontent">
Get a list of all headers of a specific name with it's name and value
separated by a column.


</div>

<div group="get_header_untouched" id="get_header_untouched-Args" class="tabcontent">

* `header` - the name of the header to search.


</div>

<div group="get_header_untouched" id="get_header_untouched-Return" class="tabcontent">

* `array` - all header values, or an empty array if the header was not found.


</div>

<div group="get_header_untouched" id="get_header_untouched-Effective smtp stage" class="tabcontent">

All of them, although it is most useful in the `preq` stage because this
is when the email body is received.


</div>

<div group="get_header_untouched" id="get_header_untouched-Examples" class="tabcontent">

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
</div>

</div>
</br>

<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> append_header </h2>

```rust,ignore
fn append_header(header: String, value: SharedObject) -> ()
fn append_header(header: String, value: String) -> ()
```

<div class="tab">
    <button
    group="append_header"
    id="link-append_header-description"
    class="tablinks active"
    onclick="openTab(event, 'append_header', 'description')">
        Description
    </button>
    <button
    group="append_header"
    id="link-append_header-Args"
    class="tablinks"
    onclick="openTab(event, 'append_header', 'Args')">
        Args
    </button>
    <button
    group="append_header"
    id="link-append_header-Effective smtp stage"
    class="tablinks"
    onclick="openTab(event, 'append_header', 'Effective smtp stage')">
        Effective smtp stage
    </button>
    <button
    group="append_header"
    id="link-append_header-Examples"
    class="tablinks"
    onclick="openTab(event, 'append_header', 'Examples')">
        Examples
    </button></div>

<div group="append_header" id="append_header-description" style="display: block;" markdown="span" class="tabcontent">
Add a new header **at the end** of the header list in the message.


</div>

<div group="append_header" id="append_header-Args" class="tabcontent">

* `header` - the name of the header to append.
* `value` - the value of the header to append.


</div>

<div group="append_header" id="append_header-Effective smtp stage" class="tabcontent">

All of them. Even though the email is not received at the current stage,
vsmtp stores new headers and will add them on top of the ones received once
the `preq` stage is reached.


</div>

<div group="append_header" id="append_header-Examples" class="tabcontent">

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
</div>

</div>
</br>

<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> prepend_header </h2>

```rust,ignore
fn prepend_header(header: String, value: String) -> ()
fn prepend_header(header: String, value: SharedObject) -> ()
```

<div class="tab">
    <button
    group="prepend_header"
    id="link-prepend_header-description"
    class="tablinks active"
    onclick="openTab(event, 'prepend_header', 'description')">
        Description
    </button>
    <button
    group="prepend_header"
    id="link-prepend_header-Args"
    class="tablinks"
    onclick="openTab(event, 'prepend_header', 'Args')">
        Args
    </button>
    <button
    group="prepend_header"
    id="link-prepend_header-Effective smtp stage"
    class="tablinks"
    onclick="openTab(event, 'prepend_header', 'Effective smtp stage')">
        Effective smtp stage
    </button>
    <button
    group="prepend_header"
    id="link-prepend_header-Examples"
    class="tablinks"
    onclick="openTab(event, 'prepend_header', 'Examples')">
        Examples
    </button></div>

<div group="prepend_header" id="prepend_header-description" style="display: block;" markdown="span" class="tabcontent">
Add a new header on top all other headers in the message.


</div>

<div group="prepend_header" id="prepend_header-Args" class="tabcontent">

* `header` - the name of the header to prepend.
* `value` - the value of the header to prepend.


</div>

<div group="prepend_header" id="prepend_header-Effective smtp stage" class="tabcontent">

All of them. Even though the email is not received at the current stage,
vsmtp stores new headers and will add them on top of the ones received once
the `preq` stage is reached.


</div>

<div group="prepend_header" id="prepend_header-Examples" class="tabcontent">

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
</div>

</div>
</br>

<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> set_header </h2>

```rust,ignore
fn set_header(header: String, value: String) -> ()
fn set_header(header: String, value: SharedObject) -> ()
```

<div class="tab">
    <button
    group="set_header"
    id="link-set_header-description"
    class="tablinks active"
    onclick="openTab(event, 'set_header', 'description')">
        Description
    </button>
    <button
    group="set_header"
    id="link-set_header-Args"
    class="tablinks"
    onclick="openTab(event, 'set_header', 'Args')">
        Args
    </button>
    <button
    group="set_header"
    id="link-set_header-Effective smtp stage"
    class="tablinks"
    onclick="openTab(event, 'set_header', 'Effective smtp stage')">
        Effective smtp stage
    </button>
    <button
    group="set_header"
    id="link-set_header-Examples"
    class="tablinks"
    onclick="openTab(event, 'set_header', 'Examples')">
        Examples
    </button></div>

<div group="set_header" id="set_header-description" style="display: block;" markdown="span" class="tabcontent">
Replace an existing header value by a new value, or append a new header
to the message.


</div>

<div group="set_header" id="set_header-Args" class="tabcontent">

* `header` - the name of the header to set or add.
* `value` - the value of the header to set or add.


</div>

<div group="set_header" id="set_header-Effective smtp stage" class="tabcontent">

All of them. Even though the email is not received at the current stage,
vsmtp stores new headers and will add them on top to the ones received once
the `preq` stage is reached.

Be aware that if you want to set a header value from the original message,
you must use `set_header` in the `preq` stage and onwards.


</div>

<div group="set_header" id="set_header-Examples" class="tabcontent">

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
</div>

</div>
</br>

<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> rename_header </h2>

```rust,ignore
fn rename_header(old: String, new: SharedObject) -> ()
fn rename_header(old: SharedObject, new: SharedObject) -> ()
fn rename_header(old: String, new: String) -> ()
fn rename_header(old: SharedObject, new: String) -> ()
```

<div class="tab">
    <button
    group="rename_header"
    id="link-rename_header-description"
    class="tablinks active"
    onclick="openTab(event, 'rename_header', 'description')">
        Description
    </button>
    <button
    group="rename_header"
    id="link-rename_header-Args"
    class="tablinks"
    onclick="openTab(event, 'rename_header', 'Args')">
        Args
    </button>
    <button
    group="rename_header"
    id="link-rename_header-Effective smtp stage"
    class="tablinks"
    onclick="openTab(event, 'rename_header', 'Effective smtp stage')">
        Effective smtp stage
    </button>
    <button
    group="rename_header"
    id="link-rename_header-Examples"
    class="tablinks"
    onclick="openTab(event, 'rename_header', 'Examples')">
        Examples
    </button></div>

<div group="rename_header" id="rename_header-description" style="display: block;" markdown="span" class="tabcontent">
Replace an existing header name by a new value.


</div>

<div group="rename_header" id="rename_header-Args" class="tabcontent">

* `old` - the name of the header to rename.
* `new` - the new new of the header.


</div>

<div group="rename_header" id="rename_header-Effective smtp stage" class="tabcontent">

All of them, although it is most useful in the `preq` stage because this
is when the email body is received.


</div>

<div group="rename_header" id="rename_header-Examples" class="tabcontent">

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
</div>

</div>
</br>

<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> mail </h2>

```rust,ignore
fn mail() -> String
```

<div class="tab">
    <button
    group="mail"
    id="link-mail-description"
    class="tablinks active"
    onclick="openTab(event, 'mail', 'description')">
        Description
    </button>
    <button
    group="mail"
    id="link-mail-Effective smtp stage"
    class="tablinks"
    onclick="openTab(event, 'mail', 'Effective smtp stage')">
        Effective smtp stage
    </button>
    <button
    group="mail"
    id="link-mail-Example"
    class="tablinks"
    onclick="openTab(event, 'mail', 'Example')">
        Example
    </button></div>

<div group="mail" id="mail-description" style="display: block;" markdown="span" class="tabcontent">
Get a copy of the whole email as a string.


</div>

<div group="mail" id="mail-Effective smtp stage" class="tabcontent">

`preq` and onwards.


</div>

<div group="mail" id="mail-Example" class="tabcontent">

```
#{
    postq: [
       action "display email content" || log("trace", `email content: ${msg::mail()}`),
    ]
}
```
</div>

</div>
</br>

<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> rm_header </h2>

```rust,ignore
fn rm_header(header: String) -> bool
fn rm_header(header: SharedObject) -> bool
```

<div class="tab">
    <button
    group="rm_header"
    id="link-rm_header-description"
    class="tablinks active"
    onclick="openTab(event, 'rm_header', 'description')">
        Description
    </button>
    <button
    group="rm_header"
    id="link-rm_header-Args"
    class="tablinks"
    onclick="openTab(event, 'rm_header', 'Args')">
        Args
    </button>
    <button
    group="rm_header"
    id="link-rm_header-Return"
    class="tablinks"
    onclick="openTab(event, 'rm_header', 'Return')">
        Return
    </button>
    <button
    group="rm_header"
    id="link-rm_header-Effective smtp stage"
    class="tablinks"
    onclick="openTab(event, 'rm_header', 'Effective smtp stage')">
        Effective smtp stage
    </button>
    <button
    group="rm_header"
    id="link-rm_header-Examples"
    class="tablinks"
    onclick="openTab(event, 'rm_header', 'Examples')">
        Examples
    </button></div>

<div group="rm_header" id="rm_header-description" style="display: block;" markdown="span" class="tabcontent">
Remove an existing header from the message.


</div>

<div group="rm_header" id="rm_header-Args" class="tabcontent">

* `header` - the name of the header to remove.


</div>

<div group="rm_header" id="rm_header-Return" class="tabcontent">

* a boolean value, true if a header has been removed, false otherwise.


</div>

<div group="rm_header" id="rm_header-Effective smtp stage" class="tabcontent">

All of them, although it is most useful in the `preq` stage because this
is when the email body is received.


</div>

<div group="rm_header" id="rm_header-Examples" class="tabcontent">

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
</div>

</div>
</br>

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
Change the sender's address in the `From` header of the message.


</div>

<div group="rw_mail_from" id="rw_mail_from-Args" class="tabcontent">

* `new_addr` - the new sender address to set.


</div>

<div group="rw_mail_from" id="rw_mail_from-Effective smtp stage" class="tabcontent">

`preq` and onwards.


</div>

<div group="rw_mail_from" id="rw_mail_from-Examples" class="tabcontent">

```
#{
    preq: [
       action "replace sender" || msg::rw_mail_from("john.server@example.com"),
    ]
}
```
</div>

</div>
</br>

<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> rw_rcpt </h2>

```rust,ignore
fn rw_rcpt(old_addr: SharedObject, new_addr: SharedObject) -> ()
fn rw_rcpt(old_addr: String, new_addr: String) -> ()
fn rw_rcpt(old_addr: SharedObject, new_addr: String) -> ()
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
Replace a recipient by an other in the `To` header of the message.


</div>

<div group="rw_rcpt" id="rw_rcpt-Args" class="tabcontent">

* `old_addr` - the recipient to replace.
* `new_addr` - the new address to use when replacing `old_addr`.


</div>

<div group="rw_rcpt" id="rw_rcpt-Effective smtp stage" class="tabcontent">

`preq` and onwards.


</div>

<div group="rw_rcpt" id="rw_rcpt-Examples" class="tabcontent">

```
#{
    preq: [
       action "rewrite recipient" || msg::rw_rcpt("john.doe@example.com", "john-mta@example.com"),
    ]
}
```
</div>

</div>
</br>

<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> add_rcpt </h2>

```rust,ignore
fn add_rcpt(new_addr: String) -> ()
fn add_rcpt(new_addr: SharedObject) -> ()
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
Add a recipient to the `To` header of the message.


</div>

<div group="add_rcpt" id="add_rcpt-Args" class="tabcontent">

* `addr` - the recipient address to add to the `To` header.


</div>

<div group="add_rcpt" id="add_rcpt-Effective smtp stage" class="tabcontent">

`preq` and onwards.


</div>

<div group="add_rcpt" id="add_rcpt-Examples" class="tabcontent">

```
#{
    preq: [
       action "update recipients" || msg::add_rcpt("john.doe@example.com"),
    ]
}
```
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
Remove a recipient from the `To` header of the message.


</div>

<div group="rm_rcpt" id="rm_rcpt-Args" class="tabcontent">

* `addr` - the recipient to remove to the `To` header.


</div>

<div group="rm_rcpt" id="rm_rcpt-Effective smtp stage" class="tabcontent">

`preq` and onwards.


</div>

<div group="rm_rcpt" id="rm_rcpt-Examples" class="tabcontent">

```
#{
    preq: [
       action "update recipients" || msg::rm_rcpt("john.doe@example.com"),
    ]
}
```
</div>

</div>
</br>
