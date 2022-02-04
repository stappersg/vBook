## Advanced scripting

### Using [RHAI](https://rhai.rs/) for programming complex actions

On top of vSL predefined actions, users can define complex rules using the [RHAI](https://rhai.rs/) scripting language.
In any case the entry point to interact with the SMTP traffic must be the first vSL "rule".

```rust
let my_string = "The question is 7x6 = 42 ?";
...

vsl.LOG(`I'm writing this string : ${my_string} into stderr`, "stderr");
```

```rust
fn my_condition(vsl) {
    let my_int = if vsl.IS_CONNECT("192.168.1.34") { 42 } else { 0 };
    if (my_int == 42) {
        true
    } else {
        false
    }
}

fn my_action1(vsl) {
    vsl.LOG_OUT(`Ok - coming from localhost`);
    vsl.CONTINUE()
}

fn my_action2(vsl, rcpts) {
    let admin = "admin@foobar.com";
    vsl.LOG_ERR(`Not from localhost. Logging the recipients's list:`);
    for rc in rcpts {
      vsl.LOG_OUT(`  - ${rc}`);
    }
    vsl.CONTINUE()
}

rule rcpt "rcpt_log" #{
    condition:  || my_condition(vsl),
    on_success: || my_action1(vsl),
    on_failure: || my_action2(vsl, rcpts),
};
```

> note that RHAI's function do not capture their external scope. If you want to use vSL's features, you must pass the module by parameter. The vsl module is available in the global scope.

### Shortcuts

If a function has no parameter, || and ( ) can be omitted.

```rust
fn my_func() {
    ...
    vsl.ACCEPT()
}

rule connect "check on connect" #{
    condition:  true,
    on_success: my_func,
    on_failure: vsl.DENY
};
```

But :

```rust
let boo = 42;
fn my_func(x, y) {
    ...
    vsl.ACCEPT()
}

rule connect "check on connect" #{
    condition: boo == 42,
    on_success: || my_func(x, y),
    on_failure: vsl.DENY
};
```
