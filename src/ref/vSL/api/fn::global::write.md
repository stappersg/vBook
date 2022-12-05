# global::write



<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

```rust
fn dump(srv: Server, mut ctx: Context, dir: String) -> ()
```

<details>
<summary markdown="span"> details </summary>

write the content of the current email with it's metadata in a json file.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

```rust
fn write(srv: Server, mut ctx: Context, message: Message, dir: String) -> ()
```

<details>
<summary markdown="span"> details </summary>

Export the current raw message to a file as an `eml` file.
The message id of the email is used to name the file.

# Args

* `dir` - the directory where to store the email. Relative to the
application path.

# Effective smtp stage

`preq` and onwards.

# Examples

```
#{
    preq: [
       action "write to file" || write("archives"),
    ]
}
```
</details>

</div>
</br>

