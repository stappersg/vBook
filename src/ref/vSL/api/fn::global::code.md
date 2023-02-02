# global::code

Predefined codes for SMTP responses.


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> c451_3_0 </h2>

```rust,ignore
fn c451_3_0() -> SharedObject
```

<details>
<summary markdown="span"> details </summary>

Multiple destination domains per transaction is unsupported code.

# Example

```
#{
    mail: [
        // Will send "451 4.3.0 Multiple destination domains per transaction is unsupported. Please try again." to the client.
        rule "deny with code" || { state::deny(code::c451_3_0()) }
    ]
}
```
</details>

</div>
</br>

<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> c451_7_1 </h2>

```rust,ignore
fn c451_7_1() -> SharedObject
```

<details>
<summary markdown="span"> details </summary>

Return a greylisting code (<https://www.rfc-editor.org/rfc/rfc6647.html#section-2.1>)

# Example

```
#{
    mail: [
        // Will send "451 4.7.1 Sender is not authorized. Please try again." to the client.
        rule "deny with code" || { state::deny(code::c451_7_1()) }
    ]
}
```
</details>

</div>
</br>

<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> c500_7_26 </h2>

```rust,ignore
fn c500_7_26() -> SharedObject
```

<details>
<summary markdown="span"> details </summary>

Return a multiple authentication failures code.

# Example

```
#{
    mail: [
        // Will send "500 5.7.26 Multiple authentication checks failed" to the client.
        rule "deny with code" || { state::deny(code::c500_7_26()) }
    ]
}
```
</details>

</div>
</br>

<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> c550_1_1 </h2>

```rust,ignore
fn c550_1_1() -> SharedObject
```

<details>
<summary markdown="span"> details </summary>

Multiple destination domains per transaction is unsupported code.

# Example

```
#{
    mail: [
        // Will send "550 5.1.1 No passing DKIM signature found" to the client.
        rule "deny with code" || { state::deny(code::c550_1_1()) }
    ]
}
```
</details>

</div>
</br>

<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> c550_7_20 </h2>

```rust,ignore
fn c550_7_20() -> SharedObject
```

<details>
<summary markdown="span"> details </summary>

Return a DKIM Failure code. (RFC 6376)
DKIM signature not found.

# Example

```
#{
    mail: [
        // Will send "550 5.7.20 No passing DKIM signature found" to the client.
        rule "deny with code" || { state::deny(code::c550_7_20()) }
    ]
}
```
</details>

</div>
</br>

<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> c550_7_21 </h2>

```rust,ignore
fn c550_7_21() -> SharedObject
```

<details>
<summary markdown="span"> details </summary>

Return a DKIM Failure code. (RFC 6376)
No acceptable DKIM signature found.

# Example

```
#{
    mail: [
        // Will send "550 5.7.21 No acceptable DKIM signature found" to the client.
        rule "deny with code" || { state::deny(code::c550_7_21()) }
    ]
}
```
</details>

</div>
</br>

<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> c550_7_22 </h2>

```rust,ignore
fn c550_7_22() -> SharedObject
```

<details>
<summary markdown="span"> details </summary>

Return a DKIM Failure code. (RFC 6376)
No valid author matched DKIM signature found.

# Example

```
#{
    mail: [
        // Will send "550 5.7.22 No valid author-matched DKIM signature found" to the client.
        rule "deny with code" || { state::deny(code::c550_7_22()) }
    ]
}
```
</details>

</div>
</br>

<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> c550_7_23 </h2>

```rust,ignore
fn c550_7_23() -> SharedObject
```

<details>
<summary markdown="span"> details </summary>

Return a SPF Failure code. (RFC 7208)
Validation failed.

# Example

```
#{
    mail: [
        // Will send "550 5.7.23 SPF validation failed" to the client.
        rule "deny with code" || { state::deny(code::c550_7_23()) }
    ]
}
```
</details>

</div>
</br>

<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> c550_7_24 </h2>

```rust,ignore
fn c550_7_24() -> SharedObject
```

<details>
<summary markdown="span"> details </summary>

Return a SPF Failure code. (RFC 7208)
Validation error.

# Example

```
#{
    mail: [
        // Will send "550 5.7.24 SPF validation error" to the client.
        rule "deny with code" || { state::deny(code::c550_7_24()) }
    ]
}
```
</details>

</div>
</br>

<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> c550_7_25 </h2>

```rust,ignore
fn c550_7_25() -> SharedObject
```

<details>
<summary markdown="span"> details </summary>

Return a reverse DNS Failure code.

# Example

```
#{
    mail: [
        // Will send "550 5.7.25 Reverse DNS validation failed" to the client.
        rule "deny with code" || { state::deny(code::c550_7_25()) }
    ]
}
```
</details>

</div>
</br>

<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> c550_7_27 </h2>

```rust,ignore
fn c550_7_27() -> SharedObject
```

<details>
<summary markdown="span"> details </summary>

Return a Null MX cod. (RFC 7505)
The sender address has a null MX record.

# Example

```
#{
    mail: [
        // Will send "550 5.7.27 Sender address has null MX" to the client.
        rule "deny with code" || { state::deny(code::c550_7_27()) }
    ]
}
```    
</details>

</div>
</br>

<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> c554_7_1 </h2>

```rust,ignore
fn c554_7_1() -> SharedObject
```

<details>
<summary markdown="span"> details </summary>

Return a relay access denied code.

# Example

```
#{
    mail: [
        // Will send "554 5.7.1 Relay access denied" to the client.
        rule "anti relay" || { state::deny(code::c554_7_1()) }
    ]
}
```
</details>

</div>
</br>

<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> c556_1_10 </h2>

```rust,ignore
fn c556_1_10() -> SharedObject
```

<details>
<summary markdown="span"> details </summary>

Return a Null MX cod. (RFC 7505)
The recipient address has a null MX record.

# Example

```
#{
    mail: [
        // Will send "556 5.1.10 Recipient address has null MX" to the client.
        rule "deny with code" || { state::deny(code::c556_1_10()) }
    ]
}
```
</details>

</div>
</br>
