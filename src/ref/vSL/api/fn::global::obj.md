# global::obj

vSL objects declaration functions.
vSL objects utility methods.
vSL objects Eq method between each other and other types.


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>get</code> local_part </h2>

```rust,ignore
fn get local_part(addr: VSLObject) -> String
```

<div class="tab">
    <button
    group="get$local_part"
    id="link-get$local_part-description"
    class="tablinks active"
    onclick="openTab(event, 'get$local_part', 'description')">
        Description
    </button>
    <button
    group="get$local_part"
    id="link-get$local_part-Args"
    class="tablinks"
    onclick="openTab(event, 'get$local_part', 'Args')">
        Args
    </button>
    <button
    group="get$local_part"
    id="link-get$local_part-Return"
    class="tablinks"
    onclick="openTab(event, 'get$local_part', 'Return')">
        Return
    </button>
    <button
    group="get$local_part"
    id="link-get$local_part-Effective smtp stage"
    class="tablinks"
    onclick="openTab(event, 'get$local_part', 'Effective smtp stage')">
        Effective smtp stage
    </button>
    <button
    group="get$local_part"
    id="link-get$local_part-Examples"
    class="tablinks"
    onclick="openTab(event, 'get$local_part', 'Examples')">
        Examples
    </button></div>

<div group="get$local_part" id="get$local_part-description" style="display: block;" markdown="span" class="tabcontent">
Get the local part of an email address.


</div>

<div group="get$local_part" id="get$local_part-Args" class="tabcontent">

* `address` - the address to extract the local part from.


</div>

<div group="get$local_part" id="get$local_part-Return" class="tabcontent">

* `String` - the local part.


</div>

<div group="get$local_part" id="get$local_part-Effective smtp stage" class="tabcontent">

All of them.


</div>

<div group="get$local_part" id="get$local_part-Examples" class="tabcontent">

```text
#{
    mail: [
        // You can also use the `get_local_part(ctx::mail_from())` syntax.
        action "display mail from identity" || {
            log("info", `received a message from ${ctx::mail_from().local_part}.`);
        }
    ],
}
```
</div>

</div>
</br>

<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> ip6 </h2>

```rust,ignore
fn ip6(ip: String) -> VSLObject
```

<div class="tab">
    <button
    group="ip6"
    id="link-ip6-description"
    class="tablinks active"
    onclick="openTab(event, 'ip6', 'description')">
        Description
    </button></div>

<div group="ip6" id="ip6-description" style="display: block;" markdown="span" class="tabcontent">
Build an ip6 address. (x:x:x:x:x:x:x:x)
</div>

</div>
</br>

<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> rg4 </h2>

```rust,ignore
fn rg4(range: String) -> VSLObject
```

<div class="tab">
    <button
    group="rg4"
    id="link-rg4-description"
    class="tablinks active"
    onclick="openTab(event, 'rg4', 'description')">
        Description
    </button></div>

<div group="rg4" id="rg4-description" style="display: block;" markdown="span" class="tabcontent">
an ip v4 range. (a.b.c.d/range)
</div>

</div>
</br>

<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> rg6 </h2>

```rust,ignore
fn rg6(range: String) -> VSLObject
```

<div class="tab">
    <button
    group="rg6"
    id="link-rg6-description"
    class="tablinks active"
    onclick="openTab(event, 'rg6', 'description')">
        Description
    </button></div>

<div group="rg6" id="rg6-description" style="display: block;" markdown="span" class="tabcontent">
an ip v6 range. (x:x:x:x:x:x:x:x/range)
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

<h2 class="func-name"> <code>fn</code> rg4 </h2>

```rust,ignore
fn rg4(range: String) -> VSLObject
```

<div class="tab">
    <button
    group="rg4"
    id="link-rg4-description"
    class="tablinks active"
    onclick="openTab(event, 'rg4', 'description')">
        Description
    </button></div>

<div group="rg4" id="rg4-description" style="display: block;" markdown="span" class="tabcontent">
an ip v4 range. (a.b.c.d/range)
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

<h2 class="func-name"> <code>get</code> local_part </h2>

```rust,ignore
fn get local_part(addr: VSLObject) -> String
```

<div class="tab">
    <button
    group="get$local_part"
    id="link-get$local_part-description"
    class="tablinks active"
    onclick="openTab(event, 'get$local_part', 'description')">
        Description
    </button>
    <button
    group="get$local_part"
    id="link-get$local_part-Args"
    class="tablinks"
    onclick="openTab(event, 'get$local_part', 'Args')">
        Args
    </button>
    <button
    group="get$local_part"
    id="link-get$local_part-Return"
    class="tablinks"
    onclick="openTab(event, 'get$local_part', 'Return')">
        Return
    </button>
    <button
    group="get$local_part"
    id="link-get$local_part-Effective smtp stage"
    class="tablinks"
    onclick="openTab(event, 'get$local_part', 'Effective smtp stage')">
        Effective smtp stage
    </button>
    <button
    group="get$local_part"
    id="link-get$local_part-Examples"
    class="tablinks"
    onclick="openTab(event, 'get$local_part', 'Examples')">
        Examples
    </button></div>

<div group="get$local_part" id="get$local_part-description" style="display: block;" markdown="span" class="tabcontent">
Get the local part of an email address.


</div>

<div group="get$local_part" id="get$local_part-Args" class="tabcontent">

* `address` - the address to extract the local part from.


</div>

<div group="get$local_part" id="get$local_part-Return" class="tabcontent">

* `String` - the local part.


</div>

<div group="get$local_part" id="get$local_part-Effective smtp stage" class="tabcontent">

All of them.


</div>

<div group="get$local_part" id="get$local_part-Examples" class="tabcontent">

```text
#{
    mail: [
        // You can also use the `get_local_part(ctx::mail_from())` syntax.
        action "display mail from identity" || {
            log("info", `received a message from ${ctx::mail_from().local_part}.`);
        }
    ],
}
```
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

<h2 class="func-name"> <code>fn</code> rg6 </h2>

```rust,ignore
fn rg6(range: String) -> VSLObject
```

<div class="tab">
    <button
    group="rg6"
    id="link-rg6-description"
    class="tablinks active"
    onclick="openTab(event, 'rg6', 'description')">
        Description
    </button></div>

<div group="rg6" id="rg6-description" style="display: block;" markdown="span" class="tabcontent">
an ip v6 range. (x:x:x:x:x:x:x:x/range)
</div>

</div>
</br>

<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> ip6 </h2>

```rust,ignore
fn ip6(ip: String) -> VSLObject
```

<div class="tab">
    <button
    group="ip6"
    id="link-ip6-description"
    class="tablinks active"
    onclick="openTab(event, 'ip6', 'description')">
        Description
    </button></div>

<div group="ip6" id="ip6-description" style="display: block;" markdown="span" class="tabcontent">
Build an ip6 address. (x:x:x:x:x:x:x:x)
</div>

</div>
</br>
