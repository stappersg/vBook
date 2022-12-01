# global::write



<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn dump(srv: Server, mut ctx: Context, dir: SharedObject) -> ()
```

<details>
<summary markdown="span"> details </summary>

write the content of the current email with it's metadata in a json file.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn dump(srv: Server, mut ctx: Context, dir: String) -> ()
```

<details>
<summary markdown="span"> details </summary>

write the content of the current email with it's metadata in a json file.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn write(srv: Server, mut ctx: Context, message: Message, dir: String) -> ()
```

<details>
<summary markdown="span"> details </summary>

write the current email to a specified folder.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn write(srv: Server, mut ctx: Context, message: Message, dir: SharedObject) -> ()
```

<details>
<summary markdown="span"> details </summary>

write the current email to a specified folder.
</details>

</div>
</br>

