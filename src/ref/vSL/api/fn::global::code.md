# global::code

Predefined codes for SMTP responses.


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> c554_7_1 </h2>

```rust,ignore
fn c554_7_1() -> SharedObject
```

<div class="tab">
    <button
    group="c554_7_1"
    id="link-c554_7_1-description"
    class="tablinks active"
    onclick="openTab(event, 'c554_7_1', 'description')">
        Description
    </button>
    <button
    group="c554_7_1"
    id="link-c554_7_1-Example"
    class="tablinks"
    onclick="openTab(event, 'c554_7_1', 'Example')">
        Example
    </button></div>

<div group="c554_7_1" id="c554_7_1-description" style="display: block;" markdown="span" class="tabcontent">
Return a relay access denied code.


</div>

<div group="c554_7_1" id="c554_7_1-Example" class="tabcontent">

```
#{
    mail: [
        // Will send "554 5.7.1 Relay access denied" to the client.
        rule "anti relay" || { state::deny(code::c554_7_1()) }
    ]
}
```
</div>

</div>
</br>

<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> c550_7_20 </h2>

```rust,ignore
fn c550_7_20() -> SharedObject
```

<div class="tab">
    <button
    group="c550_7_20"
    id="link-c550_7_20-description"
    class="tablinks active"
    onclick="openTab(event, 'c550_7_20', 'description')">
        Description
    </button>
    <button
    group="c550_7_20"
    id="link-c550_7_20-Example"
    class="tablinks"
    onclick="openTab(event, 'c550_7_20', 'Example')">
        Example
    </button></div>

<div group="c550_7_20" id="c550_7_20-description" style="display: block;" markdown="span" class="tabcontent">
Return a DKIM Failure code. (RFC 6376)
DKIM signature not found.


</div>

<div group="c550_7_20" id="c550_7_20-Example" class="tabcontent">

```
#{
    mail: [
        // Will send "550 5.7.20 No passing DKIM signature found" to the client.
        rule "deny with code" || { state::deny(code::c550_7_20()) }
    ]
}
```
</div>

</div>
</br>

<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> c550_7_21 </h2>

```rust,ignore
fn c550_7_21() -> SharedObject
```

<div class="tab">
    <button
    group="c550_7_21"
    id="link-c550_7_21-description"
    class="tablinks active"
    onclick="openTab(event, 'c550_7_21', 'description')">
        Description
    </button>
    <button
    group="c550_7_21"
    id="link-c550_7_21-Example"
    class="tablinks"
    onclick="openTab(event, 'c550_7_21', 'Example')">
        Example
    </button></div>

<div group="c550_7_21" id="c550_7_21-description" style="display: block;" markdown="span" class="tabcontent">
Return a DKIM Failure code. (RFC 6376)
No acceptable DKIM signature found.


</div>

<div group="c550_7_21" id="c550_7_21-Example" class="tabcontent">

```
#{
    mail: [
        // Will send "550 5.7.21 No acceptable DKIM signature found" to the client.
        rule "deny with code" || { state::deny(code::c550_7_21()) }
    ]
}
```
</div>

</div>
</br>

<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> c550_7_22 </h2>

```rust,ignore
fn c550_7_22() -> SharedObject
```

<div class="tab">
    <button
    group="c550_7_22"
    id="link-c550_7_22-description"
    class="tablinks active"
    onclick="openTab(event, 'c550_7_22', 'description')">
        Description
    </button>
    <button
    group="c550_7_22"
    id="link-c550_7_22-Example"
    class="tablinks"
    onclick="openTab(event, 'c550_7_22', 'Example')">
        Example
    </button></div>

<div group="c550_7_22" id="c550_7_22-description" style="display: block;" markdown="span" class="tabcontent">
Return a DKIM Failure code. (RFC 6376)
No valid author matched DKIM signature found.


</div>

<div group="c550_7_22" id="c550_7_22-Example" class="tabcontent">

```
#{
    mail: [
        // Will send "550 5.7.22 No valid author-matched DKIM signature found" to the client.
        rule "deny with code" || { state::deny(code::c550_7_22()) }
    ]
}
```
</div>

</div>
</br>

<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> c550_7_23 </h2>

```rust,ignore
fn c550_7_23() -> SharedObject
```

<div class="tab">
    <button
    group="c550_7_23"
    id="link-c550_7_23-description"
    class="tablinks active"
    onclick="openTab(event, 'c550_7_23', 'description')">
        Description
    </button>
    <button
    group="c550_7_23"
    id="link-c550_7_23-Example"
    class="tablinks"
    onclick="openTab(event, 'c550_7_23', 'Example')">
        Example
    </button></div>

<div group="c550_7_23" id="c550_7_23-description" style="display: block;" markdown="span" class="tabcontent">
Return a SPF Failure code. (RFC 7208)
Validation failed.


</div>

<div group="c550_7_23" id="c550_7_23-Example" class="tabcontent">

```
#{
    mail: [
        // Will send "550 5.7.23 SPF validation failed" to the client.
        rule "deny with code" || { state::deny(code::c550_7_23()) }
    ]
}
```
</div>

</div>
</br>

<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> c550_7_24 </h2>

```rust,ignore
fn c550_7_24() -> SharedObject
```

<div class="tab">
    <button
    group="c550_7_24"
    id="link-c550_7_24-description"
    class="tablinks active"
    onclick="openTab(event, 'c550_7_24', 'description')">
        Description
    </button>
    <button
    group="c550_7_24"
    id="link-c550_7_24-Example"
    class="tablinks"
    onclick="openTab(event, 'c550_7_24', 'Example')">
        Example
    </button></div>

<div group="c550_7_24" id="c550_7_24-description" style="display: block;" markdown="span" class="tabcontent">
Return a SPF Failure code. (RFC 7208)
Validation error.


</div>

<div group="c550_7_24" id="c550_7_24-Example" class="tabcontent">

```
#{
    mail: [
        // Will send "550 5.7.24 SPF validation error" to the client.
        rule "deny with code" || { state::deny(code::c550_7_24()) }
    ]
}
```
</div>

</div>
</br>

<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> c550_7_25 </h2>

```rust,ignore
fn c550_7_25() -> SharedObject
```

<div class="tab">
    <button
    group="c550_7_25"
    id="link-c550_7_25-description"
    class="tablinks active"
    onclick="openTab(event, 'c550_7_25', 'description')">
        Description
    </button>
    <button
    group="c550_7_25"
    id="link-c550_7_25-Example"
    class="tablinks"
    onclick="openTab(event, 'c550_7_25', 'Example')">
        Example
    </button></div>

<div group="c550_7_25" id="c550_7_25-description" style="display: block;" markdown="span" class="tabcontent">
Return a reverse DNS Failure code.


</div>

<div group="c550_7_25" id="c550_7_25-Example" class="tabcontent">

```
#{
    mail: [
        // Will send "550 5.7.25 Reverse DNS validation failed" to the client.
        rule "deny with code" || { state::deny(code::c550_7_25()) }
    ]
}
```
</div>

</div>
</br>

<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> c500_7_26 </h2>

```rust,ignore
fn c500_7_26() -> SharedObject
```

<div class="tab">
    <button
    group="c500_7_26"
    id="link-c500_7_26-description"
    class="tablinks active"
    onclick="openTab(event, 'c500_7_26', 'description')">
        Description
    </button>
    <button
    group="c500_7_26"
    id="link-c500_7_26-Example"
    class="tablinks"
    onclick="openTab(event, 'c500_7_26', 'Example')">
        Example
    </button></div>

<div group="c500_7_26" id="c500_7_26-description" style="display: block;" markdown="span" class="tabcontent">
Return a multiple authentication failures code.


</div>

<div group="c500_7_26" id="c500_7_26-Example" class="tabcontent">

```
#{
    mail: [
        // Will send "500 5.7.26 Multiple authentication checks failed" to the client.
        rule "deny with code" || { state::deny(code::c500_7_26()) }
    ]
}
```
</div>

</div>
</br>

<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> c550_7_27 </h2>

```rust,ignore
fn c550_7_27() -> SharedObject
```

<div class="tab">
    <button
    group="c550_7_27"
    id="link-c550_7_27-description"
    class="tablinks active"
    onclick="openTab(event, 'c550_7_27', 'description')">
        Description
    </button>
    <button
    group="c550_7_27"
    id="link-c550_7_27-Example"
    class="tablinks"
    onclick="openTab(event, 'c550_7_27', 'Example')">
        Example
    </button></div>

<div group="c550_7_27" id="c550_7_27-description" style="display: block;" markdown="span" class="tabcontent">
Return a Null MX cod. (RFC 7505)
The sender address has a null MX record.


</div>

<div group="c550_7_27" id="c550_7_27-Example" class="tabcontent">

```
#{
    mail: [
        // Will send "550 5.7.27 Sender address has null MX" to the client.
        rule "deny with code" || { state::deny(code::c550_7_27()) }
    ]
}
```
</div>

</div>
</br>

<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> c556_1_10 </h2>

```rust,ignore
fn c556_1_10() -> SharedObject
```

<div class="tab">
    <button
    group="c556_1_10"
    id="link-c556_1_10-description"
    class="tablinks active"
    onclick="openTab(event, 'c556_1_10', 'description')">
        Description
    </button>
    <button
    group="c556_1_10"
    id="link-c556_1_10-Example"
    class="tablinks"
    onclick="openTab(event, 'c556_1_10', 'Example')">
        Example
    </button></div>

<div group="c556_1_10" id="c556_1_10-description" style="display: block;" markdown="span" class="tabcontent">
Return a Null MX cod. (RFC 7505)
The recipient address has a null MX record.


</div>

<div group="c556_1_10" id="c556_1_10-Example" class="tabcontent">

```
#{
    mail: [
        // Will send "556 5.1.10 Recipient address has null MX" to the client.
        rule "deny with code" || { state::deny(code::c556_1_10()) }
    ]
}
```
</div>

</div>
</br>

<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> c451_7_1 </h2>

```rust,ignore
fn c451_7_1() -> SharedObject
```

<div class="tab">
    <button
    group="c451_7_1"
    id="link-c451_7_1-description"
    class="tablinks active"
    onclick="openTab(event, 'c451_7_1', 'description')">
        Description
    </button>
    <button
    group="c451_7_1"
    id="link-c451_7_1-Example"
    class="tablinks"
    onclick="openTab(event, 'c451_7_1', 'Example')">
        Example
    </button></div>

<div group="c451_7_1" id="c451_7_1-description" style="display: block;" markdown="span" class="tabcontent">
Return a greylisting code (<https://www.rfc-editor.org/rfc/rfc6647.html#section-2.1>)


</div>

<div group="c451_7_1" id="c451_7_1-Example" class="tabcontent">

```
#{
    mail: [
        // Will send "451 4.7.1 Sender is not authorized. Please try again." to the client.
        rule "deny with code" || { state::deny(code::c451_7_1()) }
    ]
}
```
</div>

</div>
</br>

<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> c451_3_0 </h2>

```rust,ignore
fn c451_3_0() -> SharedObject
```

<div class="tab">
    <button
    group="c451_3_0"
    id="link-c451_3_0-description"
    class="tablinks active"
    onclick="openTab(event, 'c451_3_0', 'description')">
        Description
    </button>
    <button
    group="c451_3_0"
    id="link-c451_3_0-Example"
    class="tablinks"
    onclick="openTab(event, 'c451_3_0', 'Example')">
        Example
    </button></div>

<div group="c451_3_0" id="c451_3_0-description" style="display: block;" markdown="span" class="tabcontent">
Multiple destination domains per transaction is unsupported code.


</div>

<div group="c451_3_0" id="c451_3_0-Example" class="tabcontent">

```
#{
    mail: [
        // Will send "451 4.3.0 Multiple destination domains per transaction is unsupported. Please try again." to the client.
        rule "deny with code" || { state::deny(code::c451_3_0()) }
    ]
}
```
</div>

</div>
</br>

<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> c550_1_1 </h2>

```rust,ignore
fn c550_1_1() -> SharedObject
```

<div class="tab">
    <button
    group="c550_1_1"
    id="link-c550_1_1-description"
    class="tablinks active"
    onclick="openTab(event, 'c550_1_1', 'description')">
        Description
    </button>
    <button
    group="c550_1_1"
    id="link-c550_1_1-Example"
    class="tablinks"
    onclick="openTab(event, 'c550_1_1', 'Example')">
        Example
    </button></div>

<div group="c550_1_1" id="c550_1_1-description" style="display: block;" markdown="span" class="tabcontent">
Multiple destination domains per transaction is unsupported code.


</div>

<div group="c550_1_1" id="c550_1_1-Example" class="tabcontent">

```
#{
    mail: [
        // Will send "550 5.1.1 No passing DKIM signature found" to the client.
        rule "deny with code" || { state::deny(code::c550_1_1()) }
    ]
}
```
</div>

</div>
</br>
