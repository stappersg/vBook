# global::unix

Utility functions to interact with unix systems.


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> user_exist </h2>

```rust,ignore
fn user_exist(name: SharedObject) -> bool
fn user_exist(name: String) -> bool
```

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

</div>
</br>
