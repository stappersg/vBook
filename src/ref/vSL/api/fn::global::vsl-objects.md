# global::vsl-objects



<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn !=(this: SharedObject, other: SharedObject) -> bool
```

<details>
<summary markdown="span"> details </summary>

Operator `!=` for `SharedObject`
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn !=(this: SharedObject, s: String) -> bool
```

<details>
<summary markdown="span"> details </summary>

Operator `!=` for `SharedObject` and `&str`
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn !=(this: String, other: SharedObject) -> bool
```

<details>
<summary markdown="span"> details </summary>

Operator `!=` for `&str` and `SharedObject`
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn ==(this: SharedObject, s: String) -> bool
```

<details>
<summary markdown="span"> details </summary>

Operator `==` for `SharedObject` and `&str`
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn ==(this: String, other: SharedObject) -> bool
```

<details>
<summary markdown="span"> details </summary>

Operator `==` for `&str` and `SharedObject`
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn ==(this: SharedObject, other: SharedObject) -> bool
```

<details>
<summary markdown="span"> details </summary>

Operator `==` for `SharedObject`
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn address(address: String) -> VSLObject
```

<details>
<summary markdown="span"> details </summary>

an email address (jones@foo.com)
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn code(code: int, text: String) -> VSLObject
```

<details>
<summary markdown="span"> details </summary>

A SMTP code with the code and message as parameter.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn code(code: int, enhanced: String, text: String) -> VSLObject
```

<details>
<summary markdown="span"> details </summary>

A SMTP code with the code and message as parameter and an enhanced code.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn contains(this: SharedObject, s: String) -> bool
```

<details>
<summary markdown="span"> details </summary>

Operator `contains`
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn contains(map: Map, object: SharedObject) -> bool
```

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn contains(this: SharedObject, other: SharedObject) -> bool
```

<details>
<summary markdown="span"> details </summary>

Operator `contains`
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn file(path: String, content_type: String) -> Array
```

<details>
<summary markdown="span"> details </summary>

the content of a file.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn fqdn(domain: String) -> VSLObject
```

<details>
<summary markdown="span"> details </summary>

a valid fully qualified domain name (foo.com)
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn get domain(addr: VSLObject) -> VSLObject
```

<details>
<summary markdown="span"> details </summary>

Get the `domain` of an email address
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn get domains(container: Array) -> Array
```

<details>
<summary markdown="span"> details </summary>

Get the `domains` of an array of email address
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn get local_part(addr: VSLObject) -> String
```

<details>
<summary markdown="span"> details </summary>

Get the `local part` of an email address
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn get local_parts(container: Array) -> Array
```

<details>
<summary markdown="span"> details </summary>

Get the user identifier of a list of email address.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn identifier(identifier: String) -> VSLObject
```

<details>
<summary markdown="span"> details </summary>

a user identifier.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn ip4(ip: String) -> VSLObject
```

<details>
<summary markdown="span"> details </summary>

Build an ip4 address. (a.b.c.d)
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn ip6(ip: String) -> VSLObject
```

<details>
<summary markdown="span"> details </summary>

Build an ip6 address. (x:x:x:x:x:x:x:x)
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn regex(regex: String) -> VSLObject
```

<details>
<summary markdown="span"> details </summary>

a regex (^[a-z0-9.]+@foo.com$)
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn rg4(range: String) -> VSLObject
```

<details>
<summary markdown="span"> details </summary>

an ip v4 range. (a.b.c.d/range)
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn rg6(range: String) -> VSLObject
```

<details>
<summary markdown="span"> details </summary>

an ip v6 range. (x:x:x:x:x:x:x:x/range)
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn to_debug(this: VSLObject) -> String
```

<details>
<summary markdown="span"> details </summary>

Convert a `SharedObject` to a debug string
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn to_string(this: VSLObject) -> String
```

<details>
<summary markdown="span"> details </summary>

Convert a `SharedObject` to a `String`
</details>

</div>
</br>

