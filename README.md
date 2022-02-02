# vBook - The vSMTP reference book

This repository contains the source of vBook, the vSMTP reference guide.
It serves as vSMTP's primary documentation and tutorial resource.

You can also read the book online for vSMTP [stable] and [beta] releases.
Be aware that issues in those versions may have been fixed in this repository already, as those releases are updated less frequently.

[stable]: https://doc.vsmtp.rs/stable/book/
[beta]: https://doc.vsmtp.rs/beta/book/

## Requirements

Building the book requires [Rust] and [mdBook]. The Rust Language runs on many platforms, and there are many ways to install it. If you want to install Rust in the most straightforward, recommended way, then use [Rustup](https://github.com/rust-lang/rustup) and/or follow the instructions on the Rust website [installation](https://www.rust-lang.org/tools/install) page.

Then you have to install [mdBook]. To get it:

```sh
cargo install mdbook
```

[Rust]: https://github.com/rust-lang/rust
[mdBook]: https://github.com/rust-lang-nursery/mdBook

## Building the book

To build the book, type:

```sh
mdbook build
```

The output will be in the `book` subdirectory. To check it out, open it in
your web browser.

_Firefox:_

```sh
firefox book/index.html                       # Linux
open -a "Firefox" book/index.html             # OS X
Start-Process "firefox.exe" .\book\index.html # Windows (PowerShell)
start firefox.exe .\book\index.html           # Windows (Cmd)
```

_Chrome:_

```bash
google-chrome book/index.html                 # Linux
open -a "Google Chrome" book/index.html       # OS X
Start-Process "chrome.exe" .\book\index.html  # Windows (PowerShell)
start chrome.exe .\book\index.html            # Windows (Cmd)
```

## Contributing

We'd love your help! Please see [CONTRIBUTING.md][contrib] to learn about the
kinds of contributions we're looking for.

[contrib]: https://github.com/viridIT/vBook/blob/main/CONTRIBUTING.md

## Licensing

vBook, vBook files and this repository are licensed under a Creative Commons Attribution-ShareAlike 4.0 International License. For further details please refer to the [License.md][License] file.

[License]: https://github.com/viridIT/vBook/blob/main/LICENSE.md
