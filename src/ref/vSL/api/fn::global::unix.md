# global::unix

Utility functions to interact with unix systems.


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
// get the HOME environment variable.
let home = unix::env(identifier("HOME"));


// "VSMTP=ENV" is malformed, this will return the unit type '()'.
let invalid = unix::env(identifier("VSMTP=ENV"));


```
</details>

</div>
</br>

<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> hostname </h2>

```rust,ignore
fn hostname() -> String
```

<details>
<summary markdown="span"> details </summary>

Get the hostname of this machine.

### Return

* `string` - the host name of the machine.

### Effective smtp stage

All of them.

### Examples

```
print(`hostname of the system: ${hostname()}`);
```
</details>

</div>
</br>

<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> user_exist </h2>

```rust,ignore
fn user_exist(name: String) -> bool
fn user_exist(name: SharedObject) -> bool
```

<details>
<summary markdown="span"> details </summary>

Check if a user exists on this server.

### Args

* `name` - the name of the user.

### Return

* `bool` - true if the user exists, false otherwise.

### Effective smtp stage

All of them.

### Examples

```
if user_exist("john") {
    print("john user found on the system.");
    # throw "a john user seems to exist on this system.";
} else {
    print("john user does not exist.");
    # return #{};
}
```
</details>

</div>
</br>
