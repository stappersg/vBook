# global::net

Predefined network ip ranges.


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> rg_192 </h2>

```rust,ignore
fn rg_192() -> SharedObject
```

<div class="tab">
    <button
    group="rg_192"
    id="link-rg_192-description"
    class="tablinks active"
    onclick="openTab(event, 'rg_192', 'description')">
        Description
    </button>
    <button
    group="rg_192"
    id="link-rg_192-Example"
    class="tablinks"
    onclick="openTab(event, 'rg_192', 'Example')">
        Example
    </button></div>

<div group="rg_192" id="rg_192-description" style="display: block;" markdown="span" class="tabcontent">
Return an ip range over "192.168.0.0/16".


</div>

<div group="rg_192" id="rg_192-Example" class="tabcontent">

```ignore
#{
    rcpt: [
        rule "anti relay" || { if ctx::client_ip() in net::rg_192() { state::next() } else { state::deny() } }
    ]
}
```
</div>

</div>
</br>

<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> rg_172 </h2>

```rust,ignore
fn rg_172() -> SharedObject
```

<div class="tab">
    <button
    group="rg_172"
    id="link-rg_172-description"
    class="tablinks active"
    onclick="openTab(event, 'rg_172', 'description')">
        Description
    </button>
    <button
    group="rg_172"
    id="link-rg_172-Example"
    class="tablinks"
    onclick="openTab(event, 'rg_172', 'Example')">
        Example
    </button></div>

<div group="rg_172" id="rg_172-description" style="display: block;" markdown="span" class="tabcontent">
Return an ip range over "172.16.0.0/12".


</div>

<div group="rg_172" id="rg_172-Example" class="tabcontent">

```ignore
#{
    rcpt: [
        rule "anti relay" || { if ctx::client_ip() in net::rg_172() { state::next() } else { state::deny() } }
    ]
}
```
</div>

</div>
</br>

<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> rg_10 </h2>

```rust,ignore
fn rg_10() -> SharedObject
```

<div class="tab">
    <button
    group="rg_10"
    id="link-rg_10-description"
    class="tablinks active"
    onclick="openTab(event, 'rg_10', 'description')">
        Description
    </button>
    <button
    group="rg_10"
    id="link-rg_10-Example"
    class="tablinks"
    onclick="openTab(event, 'rg_10', 'Example')">
        Example
    </button></div>

<div group="rg_10" id="rg_10-description" style="display: block;" markdown="span" class="tabcontent">
Return an ip range over "10.0.0.0/8".


</div>

<div group="rg_10" id="rg_10-Example" class="tabcontent">

```ignore
#{
    rcpt: [
        rule "anti relay" || { if ctx::client_ip() in net::rg_10() { state::next() } else { state::deny() } }
    ]
}
```
</div>

</div>
</br>

<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> non_routable </h2>

```rust,ignore
fn non_routable() -> Array
```

<div class="tab">
    <button
    group="non_routable"
    id="link-non_routable-description"
    class="tablinks active"
    onclick="openTab(event, 'non_routable', 'description')">
        Description
    </button></div>

<div group="non_routable" id="non_routable-description" style="display: block;" markdown="span" class="tabcontent">
Return a list of non routable networks (net_192, net_172, and net_10).
</div>

</div>
</br>
