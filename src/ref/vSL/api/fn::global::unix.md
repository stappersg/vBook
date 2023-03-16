# global::unix

Utility functions to interact with unix systems.


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> user_exist </h2>

```rust,ignore
fn user_exist(name: SharedObject) -> bool
fn user_exist(name: String) -> bool
```

<div class="tab">
    <button
    group="user_exist"
    id="link-user_exist-description"
    class="tablinks active"
    onclick="openTab(event, 'user_exist', 'description')">
        Description
    </button>
    <button
    group="user_exist"
    id="link-user_exist-Args"
    class="tablinks"
    onclick="openTab(event, 'user_exist', 'Args')">
        Args
    </button>
    <button
    group="user_exist"
    id="link-user_exist-Return"
    class="tablinks"
    onclick="openTab(event, 'user_exist', 'Return')">
        Return
    </button>
    <button
    group="user_exist"
    id="link-user_exist-Effective smtp stage"
    class="tablinks"
    onclick="openTab(event, 'user_exist', 'Effective smtp stage')">
        Effective smtp stage
    </button>
    <button
    group="user_exist"
    id="link-user_exist-Examples"
    class="tablinks"
    onclick="openTab(event, 'user_exist', 'Examples')">
        Examples
    </button>
    <button
    group="user_exist"
    id="link-user_exist-throw "a john user seems to exist on this system.";"
    class="tablinks"
    onclick="openTab(event, 'user_exist', 'throw "a john user seems to exist on this system.";')">
        throw "a john user seems to exist on this system.";
    </button>
    <button
    group="user_exist"
    id="link-user_exist-return #{};"
    class="tablinks"
    onclick="openTab(event, 'user_exist', 'return #{};')">
        return #{};
    </button></div>

<div group="user_exist" id="user_exist-description" style="display: block;" markdown="span" class="tabcontent">
Check if a user exists on this server.


</div>

<div group="user_exist" id="user_exist-Args" class="tabcontent">

* `name` - the name of the user.


</div>

<div group="user_exist" id="user_exist-Return" class="tabcontent">

* `bool` - true if the user exists, false otherwise.


</div>

<div group="user_exist" id="user_exist-Effective smtp stage" class="tabcontent">

All of them.


</div>

<div group="user_exist" id="user_exist-Examples" class="tabcontent">

```
if user_exist("john") {
    print("john user found on the system.");

</div>

<div group="user_exist" id="user_exist-throw "a john user seems to exist on this system.";" class="tabcontent">
} else {
    print("john user does not exist.");

</div>

<div group="user_exist" id="user_exist-return #{};" class="tabcontent">
}
```
</div>

</div>
</br>

<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> hostname </h2>

```rust,ignore
fn hostname() -> String
```

<div class="tab">
    <button
    group="hostname"
    id="link-hostname-description"
    class="tablinks active"
    onclick="openTab(event, 'hostname', 'description')">
        Description
    </button>
    <button
    group="hostname"
    id="link-hostname-Return"
    class="tablinks"
    onclick="openTab(event, 'hostname', 'Return')">
        Return
    </button>
    <button
    group="hostname"
    id="link-hostname-Effective smtp stage"
    class="tablinks"
    onclick="openTab(event, 'hostname', 'Effective smtp stage')">
        Effective smtp stage
    </button>
    <button
    group="hostname"
    id="link-hostname-Examples"
    class="tablinks"
    onclick="openTab(event, 'hostname', 'Examples')">
        Examples
    </button></div>

<div group="hostname" id="hostname-description" style="display: block;" markdown="span" class="tabcontent">
Get the hostname of this machine.


</div>

<div group="hostname" id="hostname-Return" class="tabcontent">

* `string` - the host name of the machine.


</div>

<div group="hostname" id="hostname-Effective smtp stage" class="tabcontent">

All of them.


</div>

<div group="hostname" id="hostname-Examples" class="tabcontent">

```
print(`hostname of the system: ${hostname()}`);
```
</div>

</div>
</br>

<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> env </h2>

```rust,ignore
fn env(variable: SharedObject) -> ?
fn env(variable: String) -> ?
```

<div class="tab">
    <button
    group="env"
    id="link-env-description"
    class="tablinks active"
    onclick="openTab(event, 'env', 'description')">
        Description
    </button>
    <button
    group="env"
    id="link-env-Args"
    class="tablinks"
    onclick="openTab(event, 'env', 'Args')">
        Args
    </button>
    <button
    group="env"
    id="link-env-Returns"
    class="tablinks"
    onclick="openTab(event, 'env', 'Returns')">
        Returns
    </button>
    <button
    group="env"
    id="link-env-Example"
    class="tablinks"
    onclick="openTab(event, 'env', 'Example')">
        Example
    </button></div>

<div group="env" id="env-description" style="display: block;" markdown="span" class="tabcontent">
Fetch an environment variable from the current process.


</div>

<div group="env" id="env-Args" class="tabcontent">

* `variable` - the variable to fetch.


</div>

<div group="env" id="env-Returns" class="tabcontent">

* `string` - the value of the fetched variable.
* `()`     - when the variable is not set,  when the variable contains the sign character (=) or the NUL character,
or that the variable does not contain valid Unicode.


</div>

<div group="env" id="env-Example" class="tabcontent">

```
// get the HOME environment variable.
let home = unix::env("HOME");


// "VSMTP=ENV" is malformed, this will return the unit type '()'.
let invalid = unix::env("VSMTP=ENV");


```
</div>

</div>
</br>
