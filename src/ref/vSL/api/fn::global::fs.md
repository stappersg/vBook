# global::fs

APIs to interact with the file system.


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> write </h2>

```rust,ignore
fn write(dir: String) -> ()
```

<div class="tab">
    <button
    group="write"
    id="link-write-description"
    class="tablinks active"
    onclick="openTab(event, 'write', 'description')">
        Description
    </button>
    <button
    group="write"
    id="link-write-Args"
    class="tablinks"
    onclick="openTab(event, 'write', 'Args')">
        Args
    </button>
    <button
    group="write"
    id="link-write-Effective smtp stage"
    class="tablinks"
    onclick="openTab(event, 'write', 'Effective smtp stage')">
        Effective smtp stage
    </button>
    <button
    group="write"
    id="link-write-Examples"
    class="tablinks"
    onclick="openTab(event, 'write', 'Examples')">
        Examples
    </button></div>

<div group="write" id="write-description" style="display: block;" markdown="span" class="tabcontent">
Export the current raw message to a file as an `eml` file.
The message id of the email is used to name the file.


</div>

<div group="write" id="write-Args" class="tabcontent">

* `dir` - the directory where to store the email. Relative to the
application path.


</div>

<div group="write" id="write-Effective smtp stage" class="tabcontent">

`preq` and onwards.


</div>

<div group="write" id="write-Examples" class="tabcontent">

```
#{
    preq: [
       action "write to file" || fs::write("archives"),
    ]
}
```
</div>

</div>
</br>

<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> dump </h2>

```rust,ignore
fn dump(dir: String) -> ()
```

<div class="tab">
    <button
    group="dump"
    id="link-dump-description"
    class="tablinks active"
    onclick="openTab(event, 'dump', 'description')">
        Description
    </button>
    <button
    group="dump"
    id="link-dump-Args"
    class="tablinks"
    onclick="openTab(event, 'dump', 'Args')">
        Args
    </button>
    <button
    group="dump"
    id="link-dump-Effective smtp stage"
    class="tablinks"
    onclick="openTab(event, 'dump', 'Effective smtp stage')">
        Effective smtp stage
    </button>
    <button
    group="dump"
    id="link-dump-Examples"
    class="tablinks"
    onclick="openTab(event, 'dump', 'Examples')">
        Examples
    </button></div>

<div group="dump" id="dump-description" style="display: block;" markdown="span" class="tabcontent">
Write the content of the current email with it's metadata in a json file.
The message id of the email is used to name the file.


</div>

<div group="dump" id="dump-Args" class="tabcontent">

* `dir` - the directory where to store the email. Relative to the
application path.


</div>

<div group="dump" id="dump-Effective smtp stage" class="tabcontent">

`preq` and onwards.


</div>

<div group="dump" id="dump-Examples" class="tabcontent">

```

#{
    preq: [
       action "write to file" || fs::dump("metadata"),
    ]
}
```
</div>

</div>
</br>
