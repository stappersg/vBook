# global::rule_state



<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn accept() -> Status
```

<details>
<summary markdown="span"> details </summary>

Return a [`Status::Accept`] with the default code associated
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn accept(code: String) -> Status
```

<details>
<summary markdown="span"> details </summary>

Return a [`Status::Accept`] with `code`

# Errors

* `code` is not a valid code
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn accept(code: SharedObject) -> Status
```

<details>
<summary markdown="span"> details </summary>

Return a [`Status::Accept`] with `code`

# Errors

* `code` is not a valid code
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn deny() -> Status
```

<details>
<summary markdown="span"> details </summary>

Return a [`Status::Deny`] with the default code associated
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn deny(code: SharedObject) -> Status
```

<details>
<summary markdown="span"> details </summary>

Return a [`Status::Deny`] with `code`

# Errors

* `code` is not a valid code
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn deny(code: String) -> Status
```

<details>
<summary markdown="span"> details </summary>

Return a [`Status::Deny`] with `code`

# Errors

* `code` is not a valid code
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn faccept() -> Status
```

<details>
<summary markdown="span"> details </summary>

Return a [`Status::Faccept`] with the default code associated
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn faccept(code: SharedObject) -> Status
```

<details>
<summary markdown="span"> details </summary>

Return a [`Status::Faccept`] with `code`

# Errors

* `code` is not a valid code
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn faccept(code: String) -> Status
```

<details>
<summary markdown="span"> details </summary>

Return a [`Status::Faccept`] with `code`

# Errors

* `code` is not a valid code
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn info(code: SharedObject) -> Status
```

<details>
<summary markdown="span"> details </summary>

Return a [`Status::Info`] with `code`

# Errors

* `code` is not a valid code
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn info(code: String) -> Status
```

<details>
<summary markdown="span"> details </summary>

Return a [`Status::Info`] with `code`

# Errors

* `code` is not a valid code
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn next() -> Status
```

<details>
<summary markdown="span"> details </summary>

Return a [`Status::Next`]
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn quarantine(queue: SharedObject) -> Status
```

<details>
<summary markdown="span"> details </summary>

Return a [`Status::Quarantine`] with `queue`

# Errors

* a mutex is poisoned
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn quarantine(queue: String) -> Status
```

<details>
<summary markdown="span"> details </summary>

Return a [`Status::Quarantine`] with `queue`

# Errors

* a mutex is poisoned
</details>

</div>
</br>

