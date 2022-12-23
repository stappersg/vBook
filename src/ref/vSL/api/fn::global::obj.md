# global::obj

vSL objects declaration functions.
vSL objects utility methods.
vSL objects Eq method between each other and other types.



<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>op</code> != </h2>

```rust,ignore
op !=(this: String, other: SharedObject) -> bool
op !=(this: SharedObject, s: String) -> bool
op !=(this: SharedObject, other: SharedObject) -> bool
```

<details>
<summary markdown="span"> details </summary>

Operator `!=` for `&str` and `SharedObject`
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>op</code> == </h2>

```rust,ignore
op ==(this: SharedObject, other: SharedObject) -> bool
op ==(this: SharedObject, s: String) -> bool
op ==(this: String, other: SharedObject) -> bool
```

<details>
<summary markdown="span"> details </summary>

Operator `==` for `SharedObject`
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> address </h2>

```rust,ignore
fn address(address: String) -> VSLObject
```

<details>
<summary markdown="span"> details </summary>

an email address (jones@foo.com)
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> code </h2>

```rust,ignore
fn code(code: int, text: String) -> VSLObject
fn code(code: int, enhanced: String, text: String) -> VSLObject
```

<details>
<summary markdown="span"> details </summary>

A SMTP code with the code and message as parameter.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> contains </h2>

```rust,ignore
fn contains(this: SharedObject, other: SharedObject) -> bool
fn contains(this: SharedObject, s: String) -> bool
fn contains(map: Map, object: SharedObject) -> bool
```

<details>
<summary markdown="span"> details </summary>

Operator `contains`
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> file </h2>

```rust,ignore
fn file(path: String, content_type: String) -> Array
```

<details>
<summary markdown="span"> details </summary>

the content of a file.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> fqdn </h2>

```rust,ignore
fn fqdn(domain: String) -> VSLObject
```

<details>
<summary markdown="span"> details </summary>

a valid fully qualified domain name (foo.com)
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>get</code> domain </h2>

```rust,ignore
fn get domain(addr: VSLObject) -> VSLObject
```

<details>
<summary markdown="span"> details </summary>

Get the domain of an email address.

# Args

* `address` - the address to extract the domain from.

# Effective smtp stage

All of them.

# Examples

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
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>get</code> domains </h2>

```rust,ignore
fn get domains(container: Array) -> Array
```

<details>
<summary markdown="span"> details </summary>

Get all domains of the recipient list.

# Args

* `rcpt_list` - the recipient list.

# Effective smtp stage

`mail` and onwards.

# Examples

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
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>get</code> local_part </h2>

```rust,ignore
fn get local_part(addr: VSLObject) -> String
```

<details>
<summary markdown="span"> details </summary>

Get the local part of an email address.

# Args

* `address` - the address to extract the local part from.

# Return

* `String` - the local part.

# Effective smtp stage

All of them.

# Examples

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
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>get</code> local_parts </h2>

```rust,ignore
fn get local_parts(container: Array) -> Array
```

<details>
<summary markdown="span"> details </summary>

Get all local parts of the recipient list.

# Args

* `rcpt_list` - the recipient list.

# Return

* `array` - array of local parts.

# Effective smtp stage

`mail` and onwards.

# Examples

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
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> identifier </h2>

```rust,ignore
fn identifier(identifier: String) -> VSLObject
```

<details>
<summary markdown="span"> details </summary>

a user identifier.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> ip4 </h2>

```rust,ignore
fn ip4(ip: String) -> VSLObject
```

<details>
<summary markdown="span"> details </summary>

Build an ip4 address. (a.b.c.d)
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> ip6 </h2>

```rust,ignore
fn ip6(ip: String) -> VSLObject
```

<details>
<summary markdown="span"> details </summary>

Build an ip6 address. (x:x:x:x:x:x:x:x)
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> regex </h2>

```rust,ignore
fn regex(regex: String) -> VSLObject
```

<details>
<summary markdown="span"> details </summary>

a regex (^[a-z0-9.]+@foo.com$)
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> rg4 </h2>

```rust,ignore
fn rg4(range: String) -> VSLObject
```

<details>
<summary markdown="span"> details </summary>

an ip v4 range. (a.b.c.d/range)
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> rg6 </h2>

```rust,ignore
fn rg6(range: String) -> VSLObject
```

<details>
<summary markdown="span"> details </summary>

an ip v6 range. (x:x:x:x:x:x:x:x/range)
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> to_debug </h2>

```rust,ignore
fn to_debug(this: VSLObject) -> String
```

<details>
<summary markdown="span"> details </summary>

Convert a `SharedObject` to a debug string
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> to_string </h2>

```rust,ignore
fn to_string(this: VSLObject) -> String
```

<details>
<summary markdown="span"> details </summary>

Convert a `SharedObject` to a `String`
</details>

</div>
</br>

