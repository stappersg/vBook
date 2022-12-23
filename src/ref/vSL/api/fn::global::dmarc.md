# global::dmarc

Domain-based message authentication, reporting and conformance implementation
specified by RFC 7489. (<https://www.rfc-editor.org/rfc/rfc7489>)



<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> check </h2>

```rust,ignore
fn check() -> Status
```

<details>
<summary markdown="span"> details </summary>

Apply the DMARC policy to the mail.

# Effective smtp stage

`preq` and onwards.

# Example

```ignore
#{
  preq: [
    rule "check dmarc" || { dmarc::check() },
  ]
}
```
</details>

</div>
</br>

