# Advanced scripting

## Using [RHAI](https://rhai.rs/) language for programming complex actions

On top of vSL predefined actions, users can define complex rules using the [RHAI](https://rhai.rs/) scripting language.

```c

action "let_example" || {
    let my_string = "The question is 7x6 = 42 ?";
    ... // do stuff

    vsl::log_stderr(`I'm writing this string : ${my_string} into stderr`);
};
```

RHAI functions can be declared and used in vSL.

```c
fn my_condition(vsl) {
    let my_int = if vsl::client_addr == "192.168.1.34" { 42 } else { 0 };
    if (my_int == 42) {
        true
    } else {
        false
    }
}

fn my_action1(vsl) {
    vsl::log_warn(`Ok - coming from localhost`);
    vsl::next()
}

fn my_action2(vsl, rcpts) {
    let admin = "admin@foobar.com";
    vsl::log(`Not from localhost. Logging the recipients's list:`, my_log);
    for rc in rcpts {
      vsl::log(`  - ${rc}`, my_log);
    }
    vsl::next()
}


run_rules!(
    #{
        ... // do stuff

        rcpt: [    
            rule "rcpt_log" || { if my_condition(vsl) { my_action1(vsl) } else { my_action2(vsl, ctx.rcpt) } },
        ]
    }
)

```

&#9998; | RHAI's function do not capture their external scope. If you want to use vSL's features, you must pass the module by parameter. The vsl module is available in the global scope.

## Importing user defined modules

External modules can be imported via the main.vsl file. 

RHAI functions are automatically exported. Thus do not forget to add the "private" keyword for internal functions. Unlike functions, variables are not exported. You must do it manually.

Example :

___mod/my_module.vsl___

```c
fn my_function() {
    let z = add_function(24);
    ... // do stuff.
}

private fn add_function(v) {
    return v + 42;
}

export const x = 42;
```

___main.vsl___

```c
import "mod/my_module" as my_mod;

my_mod::my_function();
print(my_mod::x);
```
