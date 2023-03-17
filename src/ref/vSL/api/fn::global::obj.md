# global::obj

vSL objects declaration functions.
vSL objects utility methods.
vSL objects Eq method between each other and other types.


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> ip4 </h2>

```rust,ignore
fn ip4(ip: String) -> VSLObject
```

<div class="tab">
    <button
    group="ip4"
    id="link-ip4-description"
    class="tablinks active"
    onclick="openTab(event, 'ip4', 'description')">
        Description
    </button></div>

<div group="ip4" id="ip4-description" style="display: block;" markdown="span" class="tabcontent">
Build an ip4 address. (a.b.c.d)
</div>

</div>
</br>

<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>get</code> domain </h2>

```rust,ignore
fn get domain(addr: VSLObject) -> VSLObject
```

<div class="tab">
    <button
    group="get$domain"
    id="link-get$domain-description"
    class="tablinks active"
    onclick="openTab(event, 'get$domain', 'description')">
        Description
    </button>
    <button
    group="get$domain"
    id="link-get$domain-Args"
    class="tablinks"
    onclick="openTab(event, 'get$domain', 'Args')">
        Args
    </button>
    <button
    group="get$domain"
    id="link-get$domain-Effective smtp stage"
    class="tablinks"
    onclick="openTab(event, 'get$domain', 'Effective smtp stage')">
        Effective smtp stage
    </button>
    <button
    group="get$domain"
    id="link-get$domain-Examples"
    class="tablinks"
    onclick="openTab(event, 'get$domain', 'Examples')">
        Examples
    </button></div>

<div group="get$domain" id="get$domain-description" style="display: block;" markdown="span" class="tabcontent">
Get the domain of an email address.


</div>

<div group="get$domain" id="get$domain-Args" class="tabcontent">

* `address` - the address to extract the domain from.


</div>

<div group="get$domain" id="get$domain-Effective smtp stage" class="tabcontent">

All of them.


</div>

<div group="get$domain" id="get$domain-Examples" class="tabcontent">

```text
#{
    mail: [
        // You can also use the `get_domain(ctx::mail_from())` syntax.
        action "display sender's domain" || {
            log("info", `received a message from domain ${ctx::mail_from().domain}.`);
        }
    ],
}
```
</div>

</div>
</br>

<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>get</code> local_parts </h2>

```rust,ignore
fn get local_parts(container: Array) -> Array
```

<div class="tab">
    <button
    group="get$local_parts"
    id="link-get$local_parts-description"
    class="tablinks active"
    onclick="openTab(event, 'get$local_parts', 'description')">
        Description
    </button>
    <button
    group="get$local_parts"
    id="link-get$local_parts-Args"
    class="tablinks"
    onclick="openTab(event, 'get$local_parts', 'Args')">
        Args
    </button>
    <button
    group="get$local_parts"
    id="link-get$local_parts-Return"
    class="tablinks"
    onclick="openTab(event, 'get$local_parts', 'Return')">
        Return
    </button>
    <button
    group="get$local_parts"
    id="link-get$local_parts-Effective smtp stage"
    class="tablinks"
    onclick="openTab(event, 'get$local_parts', 'Effective smtp stage')">
        Effective smtp stage
    </button>
    <button
    group="get$local_parts"
    id="link-get$local_parts-Examples"
    class="tablinks"
    onclick="openTab(event, 'get$local_parts', 'Examples')">
        Examples
    </button></div>

<div group="get$local_parts" id="get$local_parts-description" style="display: block;" markdown="span" class="tabcontent">
Get all local parts of the recipient list.


</div>

<div group="get$local_parts" id="get$local_parts-Args" class="tabcontent">

* `rcpt_list` - the recipient list.


</div>

<div group="get$local_parts" id="get$local_parts-Return" class="tabcontent">

* `array` - array of local parts.


</div>

<div group="get$local_parts" id="get$local_parts-Effective smtp stage" class="tabcontent">

`mail` and onwards.


</div>

<div group="get$local_parts" id="get$local_parts-Examples" class="tabcontent">

```text
#{
    mail: [
        action "display recipients usernames" || {
            print("list of recipients user names:");

            // You can also use the `get_local_parts(ctx::rcpt_list())` syntax.
            for user in ctx::rcpt_list().local_parts {
                print(`- ${user}`);
            }
        }
    ],
}
```
</div>

</div>
</br>

<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>op</code> != </h2>

```rust,ignore
op !=(this: SharedObject, s: String) -> bool
op !=(this: SharedObject, other: SharedObject) -> bool
op !=(this: String, other: SharedObject) -> bool
```

<div class="tab">
    <button
    group="!="
    id="link-!=-description"
    class="tablinks active"
    onclick="openTab(event, '!=', 'description')">
        Description
    </button></div>

<div group="!=" id="!=-description" style="display: block;" markdown="span" class="tabcontent">
Operator `!=` for `SharedObject` and `&str`
</div>

</div>
</br>

<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>op</code> == </h2>

```rust,ignore
op ==(this: String, other: SharedObject) -> bool
op ==(this: SharedObject, s: String) -> bool
op ==(this: SharedObject, other: SharedObject) -> bool
```

<div class="tab">
    <button
    group="=="
    id="link-==-description"
    class="tablinks active"
    onclick="openTab(event, '==', 'description')">
        Description
    </button></div>

<div group="==" id="==-description" style="display: block;" markdown="span" class="tabcontent">
Operator `==` for `&str` and `SharedObject`
</div>

</div>
</br>

<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> fqdn </h2>

```rust,ignore
fn fqdn(domain: String) -> VSLObject
```

<div class="tab">
    <button
    group="fqdn"
    id="link-fqdn-description"
    class="tablinks active"
    onclick="openTab(event, 'fqdn', 'description')">
        Description
    </button></div>

<div group="fqdn" id="fqdn-description" style="display: block;" markdown="span" class="tabcontent">
a valid fully qualified domain name (foo.com)
</div>

</div>
</br>

<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> regex </h2>

```rust,ignore
fn regex(regex: String) -> VSLObject
```

<div class="tab">
    <button
    group="regex"
    id="link-regex-description"
    class="tablinks active"
    onclick="openTab(event, 'regex', 'description')">
        Description
    </button></div>

<div group="regex" id="regex-description" style="display: block;" markdown="span" class="tabcontent">
a regex (^[a-z0-9.]+@foo.com$)
</div>

</div>
</br>

<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> file </h2>

```rust,ignore
fn file(path: String, content_type: String) -> Array
```

<div class="tab">
    <button
    group="file"
    id="link-file-description"
    class="tablinks active"
    onclick="openTab(event, 'file', 'description')">
        Description
    </button></div>

<div group="file" id="file-description" style="display: block;" markdown="span" class="tabcontent">
the content of a file.
</div>

</div>
</br>

<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> identifier </h2>

```rust,ignore
fn identifier(identifier: String) -> VSLObject
```

<div class="tab">
    <button
    group="identifier"
    id="link-identifier-description"
    class="tablinks active"
    onclick="openTab(event, 'identifier', 'description')">
        Description
    </button></div>

<div group="identifier" id="identifier-description" style="display: block;" markdown="span" class="tabcontent">
a user identifier.
</div>

</div>
</br>

<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> code </h2>

```rust,ignore
fn code(code: int, text: String) -> VSLObject
fn code(code: int, enhanced: String, text: String) -> VSLObject
```

<div class="tab">
    <button
    group="code"
    id="link-code-description"
    class="tablinks active"
    onclick="openTab(event, 'code', 'description')">
        Description
    </button></div>

<div group="code" id="code-description" style="display: block;" markdown="span" class="tabcontent">
A SMTP code with the code and message as parameter.

```ignore
let code = code(250, "Ok");
let enhanced = code(451, "5.7.3", "STARTTLS is required to send mail");
```
</div>

</div>
</br>

<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>op</code> != </h2>

```rust,ignore
op !=(this: SharedObject, s: String) -> bool
op !=(this: SharedObject, other: SharedObject) -> bool
op !=(this: String, other: SharedObject) -> bool
```

<div class="tab">
    <button
    group="!="
    id="link-!=-description"
    class="tablinks active"
    onclick="openTab(event, '!=', 'description')">
        Description
    </button></div>

<div group="!=" id="!=-description" style="display: block;" markdown="span" class="tabcontent">
Operator `!=` for `SharedObject` and `&str`
</div>

</div>
</br>

<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> address </h2>

```rust,ignore
fn address(address: String) -> VSLObject
```

<div class="tab">
    <button
    group="address"
    id="link-address-description"
    class="tablinks active"
    onclick="openTab(event, 'address', 'description')">
        Description
    </button></div>

<div group="address" id="address-description" style="display: block;" markdown="span" class="tabcontent">
an email address (jones@foo.com)
</div>

</div>
</br>

<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> ip4 </h2>

```rust,ignore
fn ip4(ip: String) -> VSLObject
```

<div class="tab">
    <button
    group="ip4"
    id="link-ip4-description"
    class="tablinks active"
    onclick="openTab(event, 'ip4', 'description')">
        Description
    </button></div>

<div group="ip4" id="ip4-description" style="display: block;" markdown="span" class="tabcontent">
Build an ip4 address. (a.b.c.d)
</div>

</div>
</br>

<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> to_string </h2>

```rust,ignore
fn to_string(this: VSLObject) -> String
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
Convert a `SharedObject` to a `String`
</div>

</div>
</br>

<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> fqdn </h2>

```rust,ignore
fn fqdn(domain: String) -> VSLObject
```

<div class="tab">
    <button
    group="fqdn"
    id="link-fqdn-description"
    class="tablinks active"
    onclick="openTab(event, 'fqdn', 'description')">
        Description
    </button></div>

<div group="fqdn" id="fqdn-description" style="display: block;" markdown="span" class="tabcontent">
a valid fully qualified domain name (foo.com)
</div>

</div>
</br>

<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>op</code> == </h2>

```rust,ignore
op ==(this: String, other: SharedObject) -> bool
op ==(this: SharedObject, s: String) -> bool
op ==(this: SharedObject, other: SharedObject) -> bool
```

<div class="tab">
    <button
    group="=="
    id="link-==-description"
    class="tablinks active"
    onclick="openTab(event, '==', 'description')">
        Description
    </button></div>

<div group="==" id="==-description" style="display: block;" markdown="span" class="tabcontent">
Operator `==` for `&str` and `SharedObject`
</div>

</div>
</br>

<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> file </h2>

```rust,ignore
fn file(path: String, content_type: String) -> Array
```

<div class="tab">
    <button
    group="file"
    id="link-file-description"
    class="tablinks active"
    onclick="openTab(event, 'file', 'description')">
        Description
    </button></div>

<div group="file" id="file-description" style="display: block;" markdown="span" class="tabcontent">
the content of a file.
</div>

</div>
</br>

<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>get</code> domain </h2>

```rust,ignore
fn get domain(addr: VSLObject) -> VSLObject
```

<div class="tab">
    <button
    group="get$domain"
    id="link-get$domain-description"
    class="tablinks active"
    onclick="openTab(event, 'get$domain', 'description')">
        Description
    </button>
    <button
    group="get$domain"
    id="link-get$domain-Args"
    class="tablinks"
    onclick="openTab(event, 'get$domain', 'Args')">
        Args
    </button>
    <button
    group="get$domain"
    id="link-get$domain-Effective smtp stage"
    class="tablinks"
    onclick="openTab(event, 'get$domain', 'Effective smtp stage')">
        Effective smtp stage
    </button>
    <button
    group="get$domain"
    id="link-get$domain-Examples"
    class="tablinks"
    onclick="openTab(event, 'get$domain', 'Examples')">
        Examples
    </button></div>

<div group="get$domain" id="get$domain-description" style="display: block;" markdown="span" class="tabcontent">
Get the domain of an email address.


</div>

<div group="get$domain" id="get$domain-Args" class="tabcontent">

* `address` - the address to extract the domain from.


</div>

<div group="get$domain" id="get$domain-Effective smtp stage" class="tabcontent">

All of them.


</div>

<div group="get$domain" id="get$domain-Examples" class="tabcontent">

```text
#{
    mail: [
        // You can also use the `get_domain(ctx::mail_from())` syntax.
        action "display sender's domain" || {
            log("info", `received a message from domain ${ctx::mail_from().domain}.`);
        }
    ],
}
```
</div>

</div>
</br>

<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> regex </h2>

```rust,ignore
fn regex(regex: String) -> VSLObject
```

<div class="tab">
    <button
    group="regex"
    id="link-regex-description"
    class="tablinks active"
    onclick="openTab(event, 'regex', 'description')">
        Description
    </button></div>

<div group="regex" id="regex-description" style="display: block;" markdown="span" class="tabcontent">
a regex (^[a-z0-9.]+@foo.com$)
</div>

</div>
</br>
