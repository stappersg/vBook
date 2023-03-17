# global::spf

Implementation of the Sender Policy Framework (SPF), described by RFC 4408. (<https://www.ietf.org/rfc/rfc4408.txt>)


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> check </h2>

```rust,ignore
fn check() -> Status
fn check(params: Map) -> Status
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
    id="link-check-Args"
    class="tablinks"
    onclick="openTab(event, 'check', 'Args')">
        Args
    </button>
    <button
    group="check"
    id="link-check-Return"
    class="tablinks"
    onclick="openTab(event, 'check', 'Return')">
        Return
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
    id="link-check-Errors"
    class="tablinks"
    onclick="openTab(event, 'check', 'Errors')">
        Errors
    </button>
    <button
    group="check"
    id="link-check-Note"
    class="tablinks"
    onclick="openTab(event, 'check', 'Note')">
        Note
    </button>
    <button
    group="check"
    id="link-check-Example"
    class="tablinks"
    onclick="openTab(event, 'check', 'Example')">
        Example
    </button></div>

<div group="check" id="check-description" style="display: block;" markdown="span" class="tabcontent">
Check spf record following the Sender Policy Framework (RFC 7208).
see <https://datatracker.ietf.org/doc/html/rfc7208>


</div>

<div group="check" id="check-Args" class="tabcontent">

* a map composed of the following parameters:
    * `header` - The header(s) where the spf results will be written.
                 Can be "spf", "auth", "both" or "none". (default: "both")
    * `policy` - Degrees of flexibility when getting spf results.
                 Can be "strict" or "soft". (default: "strict")
                 A "soft" policy will let softfail pass while a "strict"
                 policy will return a deny if the results are not "pass".


</div>

<div group="check" id="check-Return" class="tabcontent">

* `deny(code550_7_23 | code550_7_24)` - an error occurred during lookup. (returned even when a softfail is received using the "strict" policy)
* `next()` - the operation succeeded.


</div>

<div group="check" id="check-Effective smtp stage" class="tabcontent">

`mail` and onwards.


</div>

<div group="check" id="check-Errors" class="tabcontent">

* The `header` argument is not valid.
* The `policy` argument is not valid.


</div>

<div group="check" id="check-Note" class="tabcontent">

`spf::check` only checks for the sender's identity, not the `helo` value.


</div>

<div group="check" id="check-Example" class="tabcontent">

```
    mail: [
       rule "check spf" || spf::check(),
    ]
}

```

```
    mail: [
        // if this check succeed, it wil return `next`.
        // if it fails, it might return `deny` with a custom code
        // (X.7.24 or X.7.25 for example)
        //
        // if you want to use the return status, just put the spf::check
        // function on the last line of your rule.
        rule "check spf 1" || {
            log("debug", `running sender policy framework on ${ctx::mail_from()} identity ...`);
            spf::check(#{ header: "spf", policy: "soft" })
        },

        // policy is set to "strict" by default.
        rule "check spf 2" || spf::check(#{ header: "both" }),
    ],
}

```
</div>

</div>
</br>

<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> check_raw </h2>

```rust,ignore
fn check_raw() -> Map
```

<div class="tab">
    <button
    group="check_raw"
    id="link-check_raw-description"
    class="tablinks active"
    onclick="openTab(event, 'check_raw', 'description')">
        Description
    </button>
    <button
    group="check_raw"
    id="link-check_raw-Return"
    class="tablinks"
    onclick="openTab(event, 'check_raw', 'Return')">
        Return
    </button>
    <button
    group="check_raw"
    id="link-check_raw-Effective smtp stage"
    class="tablinks"
    onclick="openTab(event, 'check_raw', 'Effective smtp stage')">
        Effective smtp stage
    </button>
    <button
    group="check_raw"
    id="link-check_raw-Note"
    class="tablinks"
    onclick="openTab(event, 'check_raw', 'Note')">
        Note
    </button>
    <button
    group="check_raw"
    id="link-check_raw-Examples"
    class="tablinks"
    onclick="openTab(event, 'check_raw', 'Examples')">
        Examples
    </button></div>

<div group="check_raw" id="check_raw-description" style="display: block;" markdown="span" class="tabcontent">
WARNING: Low level API, use `spf::check` instead if you do not need
to peek inside the spf result data.

Check spf record following the Sender Policy Framework (RFC 7208).
see <https://datatracker.ietf.org/doc/html/rfc7208>


</div>

<div group="check_raw" id="check_raw-Return" class="tabcontent">

* `map` - the result of the spf check, contains the `result`, `mechanism` and `problem` keys.


</div>

<div group="check_raw" id="check_raw-Effective smtp stage" class="tabcontent">

`mail` and onwards.


</div>

<div group="check_raw" id="check_raw-Note" class="tabcontent">

`spf::check` only checks for the sender's identity, not the `helo` value.


</div>

<div group="check_raw" id="check_raw-Examples" class="tabcontent">

```text
#{
    mail: [
       rule "check spf relay" || {
            const spf = spf::check_raw();

            log("info", `spf results: ${spf.result}, mechanism: ${spf.mechanism}, problem: ${spf.problem}`)
        },
    ]
}
```
</div>

</div>
</br>
