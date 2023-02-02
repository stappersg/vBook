# global::cmd

This module exposes the `cmd` function, allowing vSMTP to execute system commands.


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> build </h2>

```rust,ignore
fn build(parameters: Map) -> Cmd
```

</div>
</br>

<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> run </h2>

```rust,ignore
fn run(cmd: Cmd) -> Map
fn run(cmd: Cmd, args: Array) -> Map
```

<details>
<summary markdown="span"> details </summary>

Execute the given command.
</details>

</div>
</br>

<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> to_debug </h2>

```rust,ignore
fn to_debug(cmd: Cmd) -> String
```

<details>
<summary markdown="span"> details </summary>


</details>

</div>
</br>

<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> to_string </h2>

```rust,ignore
fn to_string(cmd: Cmd) -> String
```

<details>
<summary markdown="span"> details </summary>


</details>

</div>
</br>
