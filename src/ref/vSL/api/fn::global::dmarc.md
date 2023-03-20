# global::dmarc

Domain-based message authentication, reporting and conformance implementation
specified by RFC 7489. (<https://www.rfc-editor.org/rfc/rfc7489>)


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> check </h2>

```rust,ignore
fn check() -> Status
```

<div class="tab">
    <button
    group="check"
    id="link-check-description"
    class="tablinks active"
    onclick="openTab(event, 'check', 'description')">
        Description
    </button>
    <button
    group="check"
    id="link-check-Effective smtp stage"
    class="tablinks"
    onclick="openTab(event, 'check', 'Effective smtp stage')">
        Effective smtp stage
    </button>
    <button
    group="check"
    id="link-check-Example"
    class="tablinks"
    onclick="openTab(event, 'check', 'Example')">
        Example
    </button></div>

<div group="check" id="check-description" style="display: block;" markdown="span" class="tabcontent">
Apply the DMARC policy to the mail.


</div>

<div group="check" id="check-Effective smtp stage" class="tabcontent">

`preq` and onwards.


</div>

<div group="check" id="check-Example" class="tabcontent">

```ignore
#{
  preq: [
    rule "check dmarc" || { dmarc::check() },
  ]
}
```
</div>

</div>
</br>
