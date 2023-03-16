# global::dns

Functions used to query the DNS.


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> lookup </h2>

```rust,ignore
fn lookup(name: String) -> Array
fn lookup(name: SharedObject) -> Array
```

<div class="tab">
    <button
    group="lookup"
    id="link-lookup-description"
    class="tablinks active"
    onclick="openTab(event, 'lookup', 'description')">
        Description
    </button>
    <button
    group="lookup"
    id="link-lookup-Args"
    class="tablinks"
    onclick="openTab(event, 'lookup', 'Args')">
        Args
    </button>
    <button
    group="lookup"
    id="link-lookup-Return"
    class="tablinks"
    onclick="openTab(event, 'lookup', 'Return')">
        Return
    </button>
    <button
    group="lookup"
    id="link-lookup-Effective smtp stage"
    class="tablinks"
    onclick="openTab(event, 'lookup', 'Effective smtp stage')">
        Effective smtp stage
    </button>
    <button
    group="lookup"
    id="link-lookup-Errors"
    class="tablinks"
    onclick="openTab(event, 'lookup', 'Errors')">
        Errors
    </button>
    <button
    group="lookup"
    id="link-lookup-Examples"
    class="tablinks"
    onclick="openTab(event, 'lookup', 'Examples')">
        Examples
    </button></div>

<div group="lookup" id="lookup-description" style="display: block;" markdown="span" class="tabcontent">
Performs a dual-stack DNS lookup for the given hostname.


</div>

<div group="lookup" id="lookup-Args" class="tabcontent">

* `host` - A valid hostname to search.


</div>

<div group="lookup" id="lookup-Return" class="tabcontent">

* `array` - an array of IPs. The array is empty if no IPs were found for the host.


</div>

<div group="lookup" id="lookup-Effective smtp stage" class="tabcontent">

All of them.


</div>

<div group="lookup" id="lookup-Errors" class="tabcontent">

* Root resolver was not found.
* Lookup failed.


</div>

<div group="lookup" id="lookup-Examples" class="tabcontent">

```
#{
  preq: [
    action "lookup recipients" || {
      let domain = "gmail.com";
      let ips = dns::lookup(domain);

      print(`ips found for ${domain}`);
      for ip in ips { print(`- ${ip}`); }
    },
  ],
}
```
</div>

</div>
</br>

<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> rlookup </h2>

```rust,ignore
fn rlookup(name: SharedObject) -> Array
fn rlookup(name: String) -> Array
```

</div>
</br>
