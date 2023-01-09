# Create plugins

> <!> This chapter is still incomplete.

vSMTP plugins are Rust crates compiled as dynamic libraries.
They can be imported directly in filtering scripts.

## Requirements

- First, make sure that [Rust and Cargo](https://www.rust-lang.org/) are installed on the system.
- The Rust community as created a cargo command called [Cargo generate](https://cargo-generate.github.io/cargo-generate/installation.html) which is used to fetch Rust project templates from Github. Make sure to install it too.
- Rhai uses a crate called [ahash] used to hash types and function signatures. To hash the plugin types with the exact same hash, the plugin must use the same seed has vSMTP. See the [`rhai-dylib`](https://github.com/rhaiscript/rhai-dylib#pitfalls) crate for more details.

## Get the plugin template

A [Rhai dylib template](https://github.com/ltabis/rhai-dylib-template) is available to easily create plugins.

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

`cargo generate` will prompt for a project name (It is recommended to use the `vsmtp-plugin-*` nomenclature to name vSMTP plugins) and a [ahash] seed. (To get more detail on what are [ahash] seeds and what they are used for, check out the [`rhai-dylib`](https://github.com/rhaiscript/rhai-dylib#pitfalls) crate)

## Overview

```rust
{{#include vsmtp-plugin-awesome/src/lib.rs}}
```
<p class="ann"> Generated Rust code using `cargo generate`, in vsmtp-plugin-awesome/src/lib.rs </p>

`cargo generate` created a basic Rust project called `vsmtp-plugin-awesome`. It contains a `module_entrypoint` function that returns a [Rhai module](https://rhai.rs/book/language/modules/index.html). Once this plugin is imported in vSMTP via the Rhai `import` statement, the 
`module_entrypoint` function is called and the returned Rhai module is used to extend `.vsl` scripts.

> The `module_entrypoint` function must be present in the crate, otherwise vSMTP will not run the plugin.

```toml
{{#include vsmtp-plugin-awesome/Cargo.toml}}
```
<p class="ann"> Generated Cargo.toml file </p>

Has specified in the manifest file generated for the project, the configured crate type is `cdylib`.

```toml
{{#include vsmtp-plugin-awesome/Cargo.toml:9}}
```

With this option, the crate can be compiled into a dynamic library, and vSMTP can access the plugin via the `module_entrypoint` function at runtime.

<!-- markdown-link-check-disable-next-line -->
[ahash]: https://crates.io/crates/ahash