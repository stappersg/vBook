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

<h2 class="func-name"> <code>op</code> == </h2>

```rust,ignore
op ==(this: SharedObject, s: String) -> bool
op ==(this: SharedObject, other: SharedObject) -> bool
op ==(this: String, other: SharedObject) -> bool
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
Operator `==` for `SharedObject` and `&str`
</div>

</div>
</br>

<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>get</code> domains </h2>

```rust,ignore
fn get domains(container: Array) -> Array
```

<div class="tab">
    <button
    group="get$domains"
    id="link-get$domains-description"
    class="tablinks active"
    onclick="openTab(event, 'get$domains', 'description')">
        Description
    </button>
    <button
    group="get$domains"
    id="link-get$domains-Args"
    class="tablinks"
    onclick="openTab(event, 'get$domains', 'Args')">
        Args
    </button>
    <button
    group="get$domains"
    id="link-get$domains-Effective smtp stage"
    class="tablinks"
    onclick="openTab(event, 'get$domains', 'Effective smtp stage')">
        Effective smtp stage
    </button>
    <button
    group="get$domains"
    id="link-get$domains-Examples"
    class="tablinks"
    onclick="openTab(event, 'get$domains', 'Examples')">
        Examples
    </button></div>

<div group="get$domains" id="get$domains-description" style="display: block;" markdown="span" class="tabcontent">
Get all domains of the recipient list.


</div>

<div group="get$domains" id="get$domains-Args" class="tabcontent">

* `rcpt_list` - the recipient list.


</div>

<div group="get$domains" id="get$domains-Effective smtp stage" class="tabcontent">

`mail` and onwards.


</div>

<div group="get$domains" id="get$domains-Examples" class="tabcontent">

```text
#{
    mail: [
        action "display recipients domains" || {
            print("list of recipients domains:");

            // You can also use the `get_domains(ctx::rcpt_list())` syntax.
            for domain in ctx::rcpt_list().domains {
                print(`- ${domain}`);
            }
        }
    ],
}
```
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

<h2 class="func-name"> <code>fn</code> to_debug </h2>

```rust,ignore
fn to_debug(this: VSLObject) -> String
```

<div class="tab">
    <button
    group="to_debug"
    id="link-to_debug-description"
    class="tablinks active"
    onclick="openTab(event, 'to_debug', 'description')">
        Description
    </button></div>

<div group="to_debug" id="to_debug-description" style="display: block;" markdown="span" class="tabcontent">
Convert a `SharedObject` to a debug string
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

<h2 class="func-name"> <code>fn</code> contains </h2>

```rust,ignore
fn contains(this: SharedObject, other: SharedObject) -> bool
fn contains(this: SharedObject, s: String) -> bool
fn contains(map: Map, object: SharedObject) -> bool
```

<div class="tab">
    <button
    group="contains"
    id="link-contains-description"
    class="tablinks active"
    onclick="openTab(event, 'contains', 'description')">
        Description
    </button></div>

<div group="contains" id="contains-description" style="display: block;" markdown="span" class="tabcontent">
Operator `contains`
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

<h2 class="func-name"> <code>op</code> == </h2>

```rust,ignore
op ==(this: SharedObject, s: String) -> bool
op ==(this: SharedObject, other: SharedObject) -> bool
op ==(this: String, other: SharedObject) -> bool
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
Operator `==` for `SharedObject` and `&str`
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

<h2 class="func-name"> <code>get</code> domains </h2>

```rust,ignore
fn get domains(container: Array) -> Array
```

<div class="tab">
    <button
    group="get$domains"
    id="link-get$domains-description"
    class="tablinks active"
    onclick="openTab(event, 'get$domains', 'description')">
        Description
    </button>
    <button
    group="get$domains"
    id="link-get$domains-Args"
    class="tablinks"
    onclick="openTab(event, 'get$domains', 'Args')">
        Args
    </button>
    <button
    group="get$domains"
    id="link-get$domains-Effective smtp stage"
    class="tablinks"
    onclick="openTab(event, 'get$domains', 'Effective smtp stage')">
        Effective smtp stage
    </button>
    <button
    group="get$domains"
    id="link-get$domains-Examples"
    class="tablinks"
    onclick="openTab(event, 'get$domains', 'Examples')">
        Examples
    </button></div>

<div group="get$domains" id="get$domains-description" style="display: block;" markdown="span" class="tabcontent">
Get all domains of the recipient list.


</div>

<div group="get$domains" id="get$domains-Args" class="tabcontent">

* `rcpt_list` - the recipient list.


</div>

<div group="get$domains" id="get$domains-Effective smtp stage" class="tabcontent">

`mail` and onwards.


</div>

<div group="get$domains" id="get$domains-Examples" class="tabcontent">

```text
#{
    mail: [
        action "display recipients domains" || {
            print("list of recipients domains:");

            // You can also use the `get_domains(ctx::rcpt_list())` syntax.
            for domain in ctx::rcpt_list().domains {
                print(`- ${domain}`);
            }
        }
    ],
}
```
</div>

</div>
</br>

<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> to_debug </h2>

```rust,ignore
fn to_debug(this: VSLObject) -> String
```

<div class="tab">
    <button
    group="to_debug"
    id="link-to_debug-description"
    class="tablinks active"
    onclick="openTab(event, 'to_debug', 'description')">
        Description
    </button></div>

<div group="to_debug" id="to_debug-description" style="display: block;" markdown="span" class="tabcontent">
Convert a `SharedObject` to a debug string
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
