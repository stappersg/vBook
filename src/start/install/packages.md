# Installing vSMTP from packages

Packages can be downloaded from the [release] section of the vSMTP github.

[release]: https://github.com/viridIT/vSMTP/releases

## Using `cargo`

<a href="https://crates.io/crates/vsmtp">
  <img src="https://img.shields.io/crates/v/vsmtp.svg"
    alt="Crates.io" />
</a>

vSMTP is published on <https://crates.io>, meaning it can be install through `cargo`

```sh
cargo install vsmtp
```

## Linux/Debian distros

The vSMTP package will be added to the Debian Repository as soon as possible.
You can also create your own package using the [cargo-deb] crate. Scripts and files used to generated the current package are available in the [tools/install] folder in vSMTP repository.

```sh
cargo deb -p vsmtp -v
```

[cargo-deb]: https://github.com/kornelski/cargo-deb

[tools/install]: https://github.com/viridIT/vSMTP/tree/main/tools/install

## Linux/RedHat distros

RPM package will come soon.

## BSD ports

`help wanted`

## Docker

Planned for the next release.
