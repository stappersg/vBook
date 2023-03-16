# global::cmd

This module exposes the `cmd` function, allowing vSMTP to execute system commands.


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> build </h2>

```rust,ignore
fn build(parameters: Map) -> Cmd
```

<div class="tab">
    <button
    group="build"
    id="link-build-description"
    class="tablinks active"
    onclick="openTab(event, 'build', 'description')">
        Description
    </button>
    <button
    group="build"
    id="link-build-Args"
    class="tablinks"
    onclick="openTab(event, 'build', 'Args')">
        Args
    </button>
    <button
    group="build"
    id="link-build-Return"
    class="tablinks"
    onclick="openTab(event, 'build', 'Return')">
        Return
    </button>
    <button
    group="build"
    id="link-build-Error"
    class="tablinks"
    onclick="openTab(event, 'build', 'Error')">
        Error
    </button>
    <button
    group="build"
    id="link-build-Example"
    class="tablinks"
    onclick="openTab(event, 'build', 'Example')">
        Example
    </button></div>

<div group="build" id="build-description" style="display: block;" markdown="span" class="tabcontent">
Create a new command executor.


</div>

<div group="build" id="build-Args" class="tabcontent">

* `parameters` - a map of the following parameters:
    * `command` - the command to execute.
    * `timeout` - a duration after which the command subprocess will be killed.
    * `args` - an array of parameters passed to the executed program. (optional)
    * `user` - a user to run the command with. (optional)
    * `group` - a group to run the command with. (optional)


</div>

<div group="build" id="build-Return" class="tabcontent">

A service used to execute the a command.


</div>

<div group="build" id="build-Error" class="tabcontent">

* The service failed to parse the command parameters.


</div>

<div group="build" id="build-Example" class="tabcontent">

```text
export const echo = cmd::build(#{
    command: "echo",
    args: ["-e", "'Hello World. \c This is vSMTP.'"],
    timeout: "10s",
});
```
</div>

</div>
</br>

<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> run </h2>

```rust,ignore
fn run(cmd: Cmd) -> Map
fn run(cmd: Cmd, args: Array) -> Map
```

<div class="tab">
    <button
    group="run"
    id="link-run-description"
    class="tablinks active"
    onclick="openTab(event, 'run', 'description')">
        Description
    </button>
    <button
    group="run"
    id="link-run-Return"
    class="tablinks"
    onclick="openTab(event, 'run', 'Return')">
        Return
    </button>
    <button
    group="run"
    id="link-run-Error"
    class="tablinks"
    onclick="openTab(event, 'run', 'Error')">
        Error
    </button>
    <button
    group="run"
    id="link-run-Example"
    class="tablinks"
    onclick="openTab(event, 'run', 'Example')">
        Example
    </button></div>

<div group="run" id="run-description" style="display: block;" markdown="span" class="tabcontent">
Execute the given command.


</div>

<div group="run" id="run-Return" class="tabcontent">

The command output.


</div>

<div group="run" id="run-Error" class="tabcontent">

* The service failed to execute the command.


</div>

<div group="run" id="run-Example" class="tabcontent">

```text
const echo = cmd::build(#{
    command: "echo",
    args: ["-e", "'Hello World. \c This is vSMTP.'"],
    timeout: "10s",
});

// the command executed will be:
// echo -e 'Hello World. \c This is vSMTP.'
echo.run();

// run the command with custom arguments (based one are replaced).
// echo -n 'Hello World.'
echo.run([ "-n", "'Hello World.'" ]);
```
</div>

</div>
</br>
