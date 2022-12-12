# global::objects



<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>op</code> != </h2>

```rust,ignore
op !=(this: SharedObject, s: String) -> bool
op !=(this: String, other: SharedObject) -> bool
op !=(this: SharedObject, other: SharedObject) -> bool
```

<details>
<summary markdown="span"> details </summary>

Operator `!=` for `SharedObject` and `&str`
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>op</code> == </h2>

```rust,ignore
op ==(this: SharedObject, s: String) -> bool
op ==(this: String, other: SharedObject) -> bool
```

<details>
<summary markdown="span"> details </summary>

Operator `==` for `SharedObject` and `&str`
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
fn contains(this: SharedObject, s: String) -> bool
fn contains(this: SharedObject, other: SharedObject) -> bool
```

<details>
<summary markdown="span"> details </summary>

Operator `contains`
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

<h2 class="func-name"> <code>fn</code> domains </h2>

```rust,ignore
fn get domains(container: Array) -> Array

```

<details>
<summary markdown="span"> details </summary>

Get the `domains` of an array of email address
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> local_parts </h2>

```rust,ignore
fn get local_parts(container: Array) -> Array

```

<details>
<summary markdown="span"> details </summary>

Get the user identifier of a list of email address.
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

