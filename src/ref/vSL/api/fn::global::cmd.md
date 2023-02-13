# global::cmd

This module exposes the `cmd` function, allowing vSMTP to execute system commands.


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> build </h2>

```rust,ignore
fn build(parameters: Map) -> Cmd
```

<details>
<summary markdown="span"> details </summary>

Create a new command executor.

# Args

* `parameters` - a map of the following parameters:
    * `command` - the command to execute.
    * `timeout` - a duration after which the command subprocess will be killed.
    * `args` - an array of parameters passed to the executed program. (optional)
    * `user` - a user to run the command with. (optional)
    * `group` - a group to run the command with. (optional)

# Return

A service used to execute the a command.

# Error

* The service failed to parse the command parameters.

# Example

```text
export const echo = cmd::build(#{
    command: "echo",
    args: ["-e", "'Hello World. \c This is vSMTP.'"],
    timeout: "10s",
});
```
</details>

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

# Return

The command output.

# Error

* The service failed to execute the command.

# Example

```text
const echo = cmd::build(#{
    command: "echo",
    args: ["-e", "'Hello World. \c This is vSMTP.'"],
    timeout: "10s",
});

// the command executed will be:
// echo -e 'Hello World. \c This is vSMTP.'
echo.run();
```
</details>

</div>
</br>
