# global::utils

Utility functions to interact with the system.


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> env </h2>

```rust,ignore
fn env(variable: SharedObject) -> ?
fn env(variable: String) -> ?
```

<details>
<summary markdown="span"> details </summary>

Fetch an environment variable from the current process.

# Args

* `variable` - the variable to fetch.

# Returns

* `string` - the value of the fetched variable.
* `()`     - when the variable is not set,  when the variable contains the sign character (=) or the NUL character,
or that the variable does not contain valid Unicode.

# Example

```
#{
  connect: [
    rule "get env variable" || {

      // get the HOME environment variable.
      let home = utils::env(identifier("HOME"));


      // "VSMTP=ENV" is malformed, this will return the unit type '()'.
      let invalid = utils::env(identifier("VSMTP=ENV"));


      // ...
    }
  ],
}
```
</details>

</div>
</br>

<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> get_root_domain </h2>

```rust,ignore
fn get_root_domain(domain: String) -> String
fn get_root_domain(domain: SharedObject) -> String
```

<details>
<summary markdown="span"> details </summary>

Get the root domain (the registrable part)

# Examples

`foo.bar.example.com` => `example.com`
</details>

</div>
</br>
