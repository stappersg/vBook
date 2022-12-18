# Command

The command plugin executes Unix shell commands directly in `vSL`.

> This is a native plugin, thus using the `cmd` function does not require an `import` statement.

## Using the plugin

This plugin exposes a single constructor function.

```rust,ignore
export const command = cmd(#{
    // Time allowed to execute the command.
    // Aborted if the timeout value is reached.
    timeout: "60s",
    // The user to execute the command with. (optional)
    user: "user",
    // The group to execute the command with. (optional)
    group: "group",
    // Name of the command to execute.
    command: "...",
    // Array of arguments to execute the command with.
    args: ["--arg1", "--arg2", "--arg3"],
});
```

> See the [Time](../filtering/time.md) chapter for more information on available time scale formats for the `timeout` field.

## Example

```rust,ignore
export const echo = cmd(#{
    timeout: "10s",
    command: "echo",
    args: ["-e", "'Hello World. \c This is vSMTP.'"],
});

// run the command.
// the command executed will be:
// echo -e 'Hello World. \c This is vSMTP.'
echo.run();
// run the command with custom arguments (based one are replaced).
// echo -n 'Hello World.'
echo.run([ "-n", "'Hello World.'" ]);
```