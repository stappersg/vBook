# global::net

Predefined network ip ranges.


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> non_routable </h2>

```rust,ignore
fn non_routable() -> Array
```

<details>
<summary markdown="span"> details </summary>

Return a list of non routable networks (net_192, net_172, and net_10).
</details>

</div>
</br>

<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> rg_10 </h2>

```rust,ignore
fn rg_10() -> SharedObject
```

<details>
<summary markdown="span"> details </summary>

Return an ip range over "10.0.0.0/8".

# Example

```ignore
#{
    rcpt: [
        rule "anti relay" || { if ctx::client_ip() in net::rg_10() { state::next() } else { state::deny() } }
    ]
}
```
</details>

</div>
</br>

<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> rg_172 </h2>

```rust,ignore
fn rg_172() -> SharedObject
```

<details>
<summary markdown="span"> details </summary>

Return an ip range over "172.16.0.0/12".

# Example

```ignore
#{
    rcpt: [
        rule "anti relay" || { if ctx::client_ip() in net::rg_172() { state::next() } else { state::deny() } }
    ]
}
```
</details>

</div>
</br>

<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> rg_192 </h2>

```rust,ignore
fn rg_192() -> SharedObject
```

<details>
<summary markdown="span"> details </summary>

Return an ip range over "192.168.0.0/16".

# Example

```ignore
#{
    rcpt: [
        rule "anti relay" || { if ctx::client_ip() in net::rg_192() { state::next() } else { state::deny() } }
    ]
}
```
</details>

</div>
</br>
