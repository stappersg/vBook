# Create plugins

> <!> This chapter is still incomplete.

vSMTP plugins are Rust crate compiled as dynamic libraries.
They can be imported directly in filtering script.

## Requirements

First, make sure that [Rust and Cargo](https://www.rust-lang.org/) are installed on your system.

The Rust community as created a cargo command called [Cargo generate](https://cargo-generate.github.io/cargo-generate/installation.html) which is used to fetch Rust project templates from Github. Make sure to install it too.

## Get the plugin template

A [Rhai dylib template](https://github.com/ltabis/rhai-dylib-template) is available to create plugins with boilerplate code already setup for you.

```sh
cargo generate --git https://github.com/ltabis/rhai-dylib-template.git
```

```
🤷   Project Name : vsmtp-plugin-awesome
🔧   Destination: /path/vsmtp-plugin-awesome ...
🔧   Generating template ...
🤷   What is the ahash key of program that will load this module ? [default: [1, 2, 3, 4]]: [1, 2, 3, 4]
[1/7]   Done: .cargo/config.toml
[2/7]   Skipped: .cargo
[3/7]   Done: .gitignore
[4/7]   Done: Cargo.toml
[5/7]   Done: README.md
[6/7]   Done: src/lib.rs
[7/7]   Skipped: src
🔧   Moving generated files into: `/path/vsmtp-plugin-awesome`...
💡   Initializing a fresh Git repository
✨   Done! New project created /path/vsmtp-plugin-awesome
```

`cargo generate` will prompt you for a project name (It is recommended to use the `vsmtp-plugin-*` nomenclature to name vSMTP plugins) and a ahash seed. (If you don't know what that is, use the default prompt. To get more detail on what are ahash seeds and what they are used for, check out the [`rhai-dylib` crate](https://github.com/rhaiscript/rhai-dylib#pitfalls))

```rust
{{#include vsmtp-plugin-awesome/src/lib.rs}}
```
<p class="ann"> Generated Rust code using `cargo generate` </p>

`cargo generate` has now created a basic Rust project to create [Rhai modules](https://rhai.rs/book/language/modules/index.html) with a `module_entrypoint` function. Basically, modules are used to add features to Rhai/vSL scripts.

```toml
{{#include vsmtp-plugin-awesome/Cargo.toml}}
```
<p class="ann"> Generated Cargo.toml file </p>

Has you can see in the manifest file generated for the project, the configured crate for your project is of type `cdylib`.

```toml
{{#include vsmtp-plugin-awesome/Cargo.toml:9}}
```

With this option your crate can be compiled into a dynamic library, and vSMTP can access your plugin via the `module_entrypoint` function.

> The `module_entrypoint` function must be present your crate, otherwise vSMTP will not run your plugin.