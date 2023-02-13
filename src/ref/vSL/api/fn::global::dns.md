# global::dns

Functions used to query the DNS.


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> lookup </h2>

```rust,ignore
fn lookup(name: String) -> Array
fn lookup(name: SharedObject) -> Array
```

<details>
<summary markdown="span"> details </summary>

Performs a dual-stack DNS lookup for the given hostname.

### Args

* `host` - A valid hostname to search.

### Return

* `array` - an array of IPs. The array is empty if no IPs were found for the host.

### Effective smtp stage

All of them.

# Errors

* Root resolver was not found.
* Lookup failed.

### Examples

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
</details>

</div>
</br>

<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> rlookup </h2>

```rust,ignore
fn rlookup(name: SharedObject) -> Array
fn rlookup(name: String) -> Array
```

<details>
<summary markdown="span"> details </summary>

Performs a reverse lookup for the given IP.

### Args

* `ip` - The IP to query.

### Return

* `array` - an array of FQDNs. The array is empty if nothing was found.

### Effective smtp stage

All of them.

# Errors

* Failed to convert the `ip` parameter from a string into an IP.
* Reverse lookup failed.

### Examples

```
#{
  connect: [
    rule "rlookup" || {
      state::accept(`250 client ip: ${"127.0.0.1"} -> ${dns::rlookup("127.0.0.1")}`);
    }
  ],
}
```
</details>

</div>
</br>
