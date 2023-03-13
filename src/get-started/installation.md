# Installation

vSMTP is a stand-alone application with few kernel interactions, it may run on any system with slight modifications. Many installation methods are available:

* by extracting a [binary package](#installation-methods) suitable for your distribution,
* by using Rust's [Cargo](#rust-cargo) tool,
* by deploying a [Docker](#docker) container.

If your system is not supported or if these installation method are not suited for your usage, you can contact us by [opening an issue on github](https://github.com/viridIT/vSMTP/issues/new/choose) or by [joining the official discord server](https://discord.gg/N8JGBRBshf).

It is possible to download and build the project from source, see the [dedicated chapter](../dev/build/source.md).

## Requirements

### Physical requirements

The current release has been tested and deployed on x86/64 and ARMv7 architectures.

### Operating systems

vSMTP is tested and deployed on the latests Ubuntu Server LTS version, but vSMTP **should be compatible** with any recent Linux distributions.

FreeBSD 13.x is supported using the latest port branch which includes Rust 1.60.

Microsoft Windows Server is not supported.
