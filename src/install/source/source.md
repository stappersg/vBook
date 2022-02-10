# Installing vSMTP from source

This page summarizes the main installation steps to install vSMTP from source.
To find detailed instructions, please check your operating system page:

- [Linux]
- [FreeBSD]
- NetBSD
- OpenBSD

[Linux]: linux.md
[FreeBSD]: freebsd.md

## Installing RUST language

vSMTP is written in Rust and must be compiled using Cargo, the Rust package manager. Rust runs on many platforms, and there are many ways to install it. If you want to install Rust in the most straightforward, recommended way, then use [Rustup] and/or follow the instructions on the [Rust website installation] page.

[Rustup]: https://github.com/rust-lang/rustup
[Rust website installation]: https://www.rust-lang.org/tools/install

> vSMTP must compiled with a Rust 1.58+ stable version. For stability and security reasons it is not recommended to run vSMTP over a Rust Beta or a Nightly version. More information about Rust release can be founded [here].

[here]: https://doc.rust-lang.org/book/appendix-07-nightly-rust.html

## vSMTP source code repository

Source code can be found on GitHub in viridIT's [vSMTP repository].

[vSMTP repository]: https://github.com/viridIT/vSMTP

```shell
git clone https://github.com/viridIT/vSMTP.git
```

You can also download a specific version without using Git mechanism in the [release folder].

[release folder]: https://github.com/viridIT/vSMTP/releases

## vSMTP compilation

Cargo (Rust package manager) will download all required dependencies and compile the source code in accordance with your environment.

```shell
cargo build --release
```

```shell
$ cargo run -V
vSMTP 1.0
ViridIT https://www.viridit.com
vSMTP : the next-gen MTA

USAGE:
    vsmtp

FLAGS:
    -h, --help       Prints help information
    -V, --version    Prints version information
```

By default Rust/Cargo use static linking to compile - all libraries required are compiled into the executable - allowing vSMTP to be a standalone application.

## Configuring OS for vSMTP

&#9762; | This version has not been tested in chroot environments.

For security purpose, vSMTP should run using a dedicated account `vsmtp:vsmtp` with minimal privileges.
vSMTP binaries and config files should located in:

- /usr/sbin/ for binaries
- /etc/vsmtp/
  - /etc/vsmtp/vsmtp.toml : the default configuration file
  - /etc/vsmtp/rules/ for rules
  - /etc/vsmtp/certs/ for certificates
- /var/spool/vsmtp/ for internal queues
- /var/log/
  - /var/log/vsmtp/ for internal logs and trace
  - /var/log/mail.log and mail.err for syslog (not implemented in current release)
- /home/~user/Maildir for local IMAP delivery

This default behavior can be changed in the vSMTP configuration file `/etc/vsmtp/vsmtp.toml` which is called at startup by the vsmtp service script.

## Minimal configuration file

/etc/?????????????



Used file for config :

[server]
domain = "negabit.com"
addr = "192.168.1.102:25"
addr_submission = "192.168.1.102:587"
addr_submissions = "192.168.1.102:465"

[logs]
file = "/var/log/vsmtp/vsmtp.log"

[logs.level]
default = "warn"
receiver = "info"
resolver = "warn"
rules = "warn"

[rules]
dir = "/etc/vsmtp/rules"

[smtps]
security_level = "May"
capath = "/etc/vsmtp/certs"
preempt_cipherlist = true
handshake_timeout = "100ms"
protocol_version = ["TLSv1.3"]

fullchain = "{capath}/certificate.crt"
private_key = "{capath}/privateKey.key"

[smtp]
rcpt_count_max = 25
disable_ehlo = false

[smtp.error]
soft_count = 5
hard_count = 10
delay = "5000ms"

[reply_codes]
Code214 = "214 my custom help message\r\n"
Code220 = "220 {domain} ESMTP Service ready\r\n"

[delivery]
spool_dir = "/var/spool/vsmtp"

[delivery.queues]
working = { capacity = 32 }
deliver = { capacity = 32 }
deferred = { retry_max = 10, cron_period = "10s" }
