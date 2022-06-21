# Advanced scripting

## Using [RHAI](https://rhai.rs/) language for programming complex actions

On top of vSL predefined actions, users can define complex rules using the [RHAI](https://rhai.rs/) scripting language.

```javascript
action "let example" || {
    let my_string = "The question is 7x6 = 42 ?";
    // ... do stuff

    log("error", `I'm writing this string : ${my_string} as an error`);
};
```

RHAI functions can be declared and used in vSL.

```javascript
fn my_condition() {
    let my_int = if ctx().client_ip == "192.168.1.34" { 42 } else { 0 };
    if (my_int == 42) {
        true
    } else {
        false
    }
}

fn my_action1() {
    log_warn(`Ok - coming from localhost`);
    next()
}

fn my_action2(rcpts) {
    let admin = "admin@foobar.com";
    log("error", `Not from localhost. Logging the recipients's list: ${my_log}`);
    for rc in rcpts {
      log("debug", `  - ${rc}`);
    }
    next()
}


#{
    // ... other rules.
    rcpt: [
        rule "rcpt log" || { if my_condition() { my_action1() } else { my_action2(ctx().rcpt_list) } },
    ]
}
```

&#9998; | RHAI's function do not capture their external scope except for  functions [(they are "pure")](https://rhai.rs/book/language/functions.html#no-access-to-external-scope). you must pass necessary variables via parameters.

## Importing user defined modules

External modules can be imported via the main.vsl file.

RHAI functions are automatically exported. Thus do not forget to add the "private" keyword for internal functions. Unlike functions, variables are not exported. You must do it manually using the `export` keyword. Check out the [Rhai Book](https://rhai.rs/book/language/modules/export.html) for more information.

Example :

```javascript
// -- mod/my_module.vsl
fn my_function() {
    let z = add_function(24);
    ... // do stuff.
}

private fn add_function(v) {
    return v + 42;
}

export const x = 42;
```

```javascript
// -- main.vsl
import "mod/my_module" as my_mod;

my_mod::my_function();
print(my_mod::x);
```
