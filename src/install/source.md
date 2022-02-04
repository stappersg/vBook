## Installing vSMTP from source

vSMTP is currently under development. There's no stable version packaged. It must be compiled from source code.

### Installing RUST language

vSMTP is written in Rust and must be compiled using Cargo, the Rust package manager. Rust runs on many platforms, and there are many ways to install it. If you want to install Rust in the most straightforward, recommended way, then use [Rustup] and/or follow the instructions on the [Rust website installation] page.

[Rustup]: https://github.com/rust-lang/rustup
[Rust website installation]: https://www.rust-lang.org/tools/install

> vSMTP is compiled with the latest Rust Stable version. For stability and security reasons it is not recommended to run vSMTP over a Rust Beta or a Nightly version. More information about Rust release can be founded [here].



### Checking dependencies

[here]: https://doc.rust-lang.org/book/appendix-07-nightly-rust.html

vSMTP requires libc libraries and GCC compiler/linker. On a Debian system these can be installed through the build-essential package.

```shell
sudo apt install build-essential
```

Advanced Package Tool, or [APT], is also required to handle the installation and removal of software on Debian, Ubuntu and other Linux distributions.

[APT]: https://www.freedesktop.org/wiki/Software/pkg-config/

```shell
sudo apt install pkg-config
```

The Transport Layer Security protocol (TLS) is provided by [OpenSSL development libraries].
The Debian package is libssl-dev package.

[OpenSSL development libraries]: https://www.openssl.org/

```shell
sudo apt install libssl-dev
```

### vSMTP source code repository

Source code can be found on GitHub in viridIT's [vSMTP repository].

```shell
git clone https://github.com/viridIT/vSMTP.git
```

You can also download a specific version without using Git mechanism in the [release folder].

[release folder]: https://github.com/viridIT/vSMTP/releases

### vSMTP compilation

Cargo (Rust package manager) will download all required dependencies and compile the source code in accordance with your environment.

[vSMTP repository]: https://github.com/viridIT/vSMTP

```shell
$ cargo build --release
[...]

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

### Configuring OS for vSMTP

&#9762; This version has not been tested in chroot environments.

#### User and group

For security purpose, vSMTP should run using a dedicated account with minimal privileges.

```shell
$ sudo adduser --system --shell /usr/sbin/nologin --no-create-home \
    --uid 9999 --group --disabled-password --disabled-login vsmtp
Adding system user 'vsmtp' (UID 9999) ...
Adding new group 'vsmtp' (GID 9999) ...
Adding new user 'vsmtp' (UID 9999) with group 'vsmtp' ...
Not creating home directory '/home/vsmtp'.
```

#### Working directories

vSMTP binaries and config files should located in:

+ /usr/sbin/ for binaries
+ /etc/vsmtp/
  + /etc/vsmtp/vsmtp.toml : the default configuration file
  + /etc/vsmtp/rules/ for rules
+ /var/spool/vsmtp/ for internal queues
+ /var/log/
  + /var/log/vsmtp/ for internal logs and trace
  + /var/log/mail.log and mail.err for syslog (not implemented in current release)
+ /home/~user/Maildir for local IMAP delivery

The vSMTP default configuration file (/etc/vsmtp/vsmtp.toml) can be changed in the vsmtp.service script.

Create the directories and change the owner and group.

```shell
sudo mkdir /etc/vsmtp /etc/vsmtp/rules /etc/vsmtp/certs /var/log/vsmtp
sudo chown -R vsmtp:vsmtp /var/log/vsmtp /etc/vsmtp/*
```

Copy the vsmtp binaries and the config files.

```shell
sudo cp ./target/release/vsmtp /usr/sbin/
sudo cp -p ./config/vsmtp.default.toml /etc/vsmtp/vsmtp.toml
```

#### MTA service

Check if you have a mail transfer agent service running and disable it.
The example below is related to a Postfix service running on port 25.

```shell
$ sudo netstat -ltpn | grep ":25"
tcp        0      0 0.0.0.0:25              0.0.0.0:*               LISTEN      39423/master

$ sudo systemctl status postfix
● postfix.service - Postfix Mail Transport Agent
     Loaded: loaded (/lib/systemd/system/postfix.service; enabled; vendor preset: enabled)
     Active: active (exited) since Fri 2021-12-10 11:10:58 CET; 5min ago
    Process: 39426 ExecStart=/bin/true (code=exited, status=0/SUCCESS)
   Main PID: 39426 (code=exited, status=0/SUCCESS)

$ sudo systemctl stop postfix

$ sudo systemctl disable postfix
Synchronizing state of postfix.service with SysV service script with /lib/systemd/systemd-sysv-install.
Executing: /lib/systemd/systemd-sysv-install disable postfix
Removed /etc/systemd/system/multi-user.target.wants/postfix.service.
```

#### Adding vSMTP as a systemd service

Copy the daemon configuration file to /etc/systemd/system.

```shell
sudo cp ./config/vsmtp.service /etc/systemd/system
```

Enable and activate vSMTP service.

```shell
$ sudo systemctl enable vsmtp.service
Created symlink /etc/systemd/system/multi-user.target.wants/vsmtp.service → /etc/systemd/system/vsmtp.service.

$ sudo systemctl start vsmtp

$ sudo systemctl status vsmtp
● vsmtp.service - vSMTP Mail Transfer Agent
     Loaded: loaded (/etc/systemd/system/vsmtp.service; enabled; vendor preset: enabled)
     Active: active (running) since Fri 2021-12-10 11:32:15 CET; 21s ago
   Main PID: 2164 (vsmtp)
      Tasks: 25 (limit: 38287)
     Memory: 39.9M
     CGroup: /system.slice/vsmtp.service
             └─2164 /usr/sbin/vsmtp -c /etc/vsmtp/vsmtp.toml

$ sudo netstat -ltpn | grep ":25"
tcp        0      0 127.0.0.1:25            0.0.0.0:*               LISTEN      39739/vsmtp
```

Connect to the vSMTP server using a netcat or a telnet client.

```shell
$ nc -4 localhost 25
220 mydomain.com Service ready
451 Timeout - closing connection.
```
