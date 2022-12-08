# Installation

vSMTP is a stand-alone application with few kernel interactions, it may run on any system with slight modifications. Many installation methods are available:

* by extracting a [binary package](#installation-methods) suitable for your distribution,
* by using Rust's [Cargo](#rust-cargo) tool,
* by deploying a [Docker](#docker) container.

If your system is not supported or if these installation method are not suited for your usage, you can contact us by [opening an issue on github](https://github.com/viridIT/vSMTP/issues/new/choose) or by [joining the official discord server](https://discord.gg/N8JGBRBshf).

You can download and build the project from source, see the [dedicated chapter](../dev/build/source.md).

## Requirements

### Physical requirements

The current release has been tested and deployed on x86/64 and ARMv7 architectures.

### Operating systems

vSMTP is tested and deployed on the latests Ubuntu Server LTS version, but vSMTP **should be compatible** with any recent Linux distributions.

FreeBSD 13.x is supported using the latest port branch which includes Rust 1.60.

Microsoft Windows Server is not supported.

## Installation methods

### Linux distros

Debian binary packages `.deb` can be downloaded from the [release] section of the vSMTP github.

[release]: https://github.com/viridIT/vSMTP/releases/latest

```sh
sudo apt install vsmtp
```

Fedora and RedHat packages are planned for future releases. `help wanted`

### BSD ports

`help wanted` ( [Issue 484](https://github.com/viridIT/vSMTP/issues/484) )

### Rust Cargo

<a href="https://crates.io/crates/vsmtp">
  <img src="https://img.shields.io/crates/v/vsmtp.svg"
    alt="crates.io" />
</a>

<!-- markdown-link-check-disable-next-line -->
vSMTP is published on <https://crates.io>. It can be installed using [cargo].

```sh
cargo install vsmtp
```

[cargo]: https://doc.rust-lang.org/cargo

### [Docker](https://hub.docker.com/repository/docker/viridit/vsmtp)

```sh
docker pull viridit/vsmtp
```
