# Installing vSMTP from source

This page summarizes the main steps to install vSMTP from source code. To find detailed instructions for your operating system, please follow the related links

- [Linux]
- [FreeBSD]
- NetBSD `help wanted`
- OpenBSD `help wanted`

[Linux]: https://vsmtp.rs/install/source/linux.html
[FreeBSD]: https://vsmtp.rs/install/source/freebsd.html

## Installing Rust language

vSMTP is written in Rust and must be compiled using Cargo, the Rust package manager. Rust runs on many platforms, and there are many ways to install it. If you want to install Rust in the most straightforward, recommended way, then use [Rustup] and/or follow the instructions on the [Rust website installation] page.

[Rustup]: https://github.com/rust-lang/rustup
[Rust website installation]: https://www.rust-lang.org/tools/install

> vSMTP must be compiled with a Rust 1.60+ stable version. For stability and security reasons it is not recommended to run vSMTP over a Rust Beta or a Nightly version. More information about Rust release can be found [here].

[here]: https://doc.rust-lang.org/book/appendix-07-nightly-rust.html

## vSMTP source code repository

Source code can be found on GitHub in viridIT's [vSMTP repository].

[vSMTP repository]: https://github.com/viridIT/vSMTP

```shell
git clone https://github.com/viridIT/vSMTP.git
```

You can also download a specific version without using Git mechanism in the [release folder].

[release folder]: https://github.com/viridIT/vSMTP/releases
