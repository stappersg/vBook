# global::time

Utilities to get the current time and date.


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> date </h2>

```rust,ignore
fn date() -> String
```

<details>
<summary markdown="span"> details </summary>

Get the current date.

### Return

* `string` - the current date.

### Effective smtp stage

All of them.

### Examples

```text
#{
    preq: [
       action "append info header" || {
            msg::append_header("X-VSMTP", `email received by ${utils::hostname()} the ${time::date()}.`);
       }
    ]
}
```
</details>

</div>
</br>

<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> now </h2>

```rust,ignore
fn now() -> String
```

<details>
<summary markdown="span"> details </summary>

Get the current time.

### Return

* `string` - the current time.

### Effective smtp stage

All of them.

### Examples

```text
#{
    preq: [
       action "append info header" || {
            msg::append_header("X-VSMTP", `email received by ${utils::hostname()} the ${time::date()} at ${time::now()}.`);
       }
    ]
}
```
</details>

</div>
</br>
