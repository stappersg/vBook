# global::dmarc



<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn dmarc_check(record: Record, rfc5322_from: String, dkim_result: Map, spf_mail_from: String, spf_result: String) -> bool
```

<details>
<summary markdown="span"> details </summary>


</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn get receiver_policy(record: Record) -> String
```

<details>
<summary markdown="span"> details </summary>


</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn get_dmarc_record(server: Server, domain: String) -> Record
```

<details>
<summary markdown="span"> details </summary>

Get a valid DMARC record for the domain.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn get_dmarc_record(server: Server, domain: SharedObject) -> Record
```

<details>
<summary markdown="span"> details </summary>

Get a valid DMARC record for the domain.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn parse_rfc5322_from(message: Message) -> SharedObject
```

<details>
<summary markdown="span"> details </summary>

Get the address of the sender in the message body, also known as RFC5322.From
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn to_debug(record: Record) -> String
```

<details>
<summary markdown="span"> details </summary>

Produce a debug output for the parsed [`dmarc::Record`]
</details>

</div>
</br>

