# global::time

Utilities to get the current time and date.


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> now </h2>

```rust,ignore
fn now() -> String
```

<div class="tab">
    <button
    group="now"
    id="link-now-description"
    class="tablinks active"
    onclick="openTab(event, 'now', 'description')">
        Description
    </button>
    <button
    group="now"
    id="link-now-Return"
    class="tablinks"
    onclick="openTab(event, 'now', 'Return')">
        Return
    </button>
    <button
    group="now"
    id="link-now-Effective smtp stage"
    class="tablinks"
    onclick="openTab(event, 'now', 'Effective smtp stage')">
        Effective smtp stage
    </button>
    <button
    group="now"
    id="link-now-Examples"
    class="tablinks"
    onclick="openTab(event, 'now', 'Examples')">
        Examples
    </button></div>

<div group="now" id="now-description" style="display: block;" markdown="span" class="tabcontent">
Get the current time.


</div>

<div group="now" id="now-Return" class="tabcontent">

* `string` - the current time.


</div>

<div group="now" id="now-Effective smtp stage" class="tabcontent">

All of them.


</div>

<div group="now" id="now-Examples" class="tabcontent">

```text
#{
    preq: [
       action "append info header" || {
            msg::append_header("X-VSMTP", `email received by ${utils::hostname()} the ${time::date()} at ${time::now()}.`);
       }
    ]
}
```
</div>

</div>
</br>

<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> date </h2>

```rust,ignore
fn date() -> String
```

<div class="tab">
    <button
    group="date"
    id="link-date-description"
    class="tablinks active"
    onclick="openTab(event, 'date', 'description')">
        Description
    </button>
    <button
    group="date"
    id="link-date-Return"
    class="tablinks"
    onclick="openTab(event, 'date', 'Return')">
        Return
    </button>
    <button
    group="date"
    id="link-date-Effective smtp stage"
    class="tablinks"
    onclick="openTab(event, 'date', 'Effective smtp stage')">
        Effective smtp stage
    </button>
    <button
    group="date"
    id="link-date-Examples"
    class="tablinks"
    onclick="openTab(event, 'date', 'Examples')">
        Examples
    </button></div>

<div group="date" id="date-description" style="display: block;" markdown="span" class="tabcontent">
Get the current date.


</div>

<div group="date" id="date-Return" class="tabcontent">

* `string` - the current date.


</div>

<div group="date" id="date-Effective smtp stage" class="tabcontent">

All of them.


</div>

<div group="date" id="date-Examples" class="tabcontent">

```text
#{
    preq: [
       action "append info header" || {
            msg::append_header("X-VSMTP", `email received by ${utils::hostname()} the ${time::date()}.`);
       }
    ]
}
```
</div>

</div>
</br>
