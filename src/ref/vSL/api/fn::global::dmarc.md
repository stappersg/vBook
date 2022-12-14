# global::dmarc



<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> dmarc_check </h2>

```rust,ignore
fn dmarc_check(record: Record, rfc5322_from: String, dkim_result: Map, spf_mail_from: String, spf_result: String) -> bool

```

<details>
<summary markdown="span"> details </summary>


</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> get_dmarc_record </h2>

```rust,ignore
fn get_dmarc_record(server: Server, domain: SharedObject) -> Record
fn get_dmarc_record(server: Server, domain: String) -> Record
```

<details>
<summary markdown="span"> details </summary>

Get a valid DMARC record for the domain.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> to_debug </h2>

```rust,ignore
fn to_debug(record: Record) -> String

```

<details>
<summary markdown="span"> details </summary>

Produce a debug output for the parsed [`dmarc::Record`]
</details>

</div>
</br>

