# global::utils

Utility functions to interact with the system.


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> get_root_domain </h2>

```rust,ignore
fn get_root_domain(domain: String) -> String
fn get_root_domain(domain: SharedObject) -> String
```

<div class="tab">
    <button
    group="get_root_domain"
    id="link-get_root_domain-description"
    class="tablinks active"
    onclick="openTab(event, 'get_root_domain', 'description')">
        Description
    </button>
    <button
    group="get_root_domain"
    id="link-get_root_domain-Examples"
    class="tablinks"
    onclick="openTab(event, 'get_root_domain', 'Examples')">
        Examples
    </button></div>

<div group="get_root_domain" id="get_root_domain-description" style="display: block;" markdown="span" class="tabcontent">
Get the root domain (the registrable part)


</div>

<div group="get_root_domain" id="get_root_domain-Examples" class="tabcontent">

`foo.bar.example.com` => `example.com`
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
#{
  connect: [
    rule "get env variable" || {

      // get the HOME environment variable.
      let home = utils::env("HOME");


      // "VSMTP=ENV" is malformed, this will return the unit type '()'.
      let invalid = utils::env("VSMTP=ENV");


      // ...
    }
  ],
}
```
</div>

</div>
</br>
