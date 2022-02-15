# Linux installation

The installation described above is for a Ubuntu Server 20.04.

## Installing RUST language

If you want to install Rust in the most straightforward, recommended way, then use [Rustup] and follow the instructions.

```shell
curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh
```

[Rustup]: https://github.com/rust-lang/rustup

## Checking dependencies

vSMTP requires libc libraries and GCC compiler/linker. On a Debian system these can be installed through the build-essential package.

```shell
sudo apt install build-essential
```

The Transport Layer Security protocol (TLS) is provided by [OpenSSL development libraries].
The Debian package is libssl-dev package.

[OpenSSL development libraries]: https://www.openssl.org/

```shell
sudo apt install libssl-dev
```

## vSMTP compilation

Cargo (Rust package manager) will download all required dependencies and compile the source code in accordance with your environment.

```shell
git clone https://github.com/viridIT/vSMTP.git
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

## Configuring the Operating System for vSMTP

For security purpose, vSMTP should run using a dedicated account with minimal privileges.

```shell
$ sudo adduser --system --shell /usr/sbin/nologin --no-create-home \
    --uid 9999 --group --disabled-password --disabled-login vsmtp
Adding system user 'vsmtp' (UID 9999) ...
Adding new group 'vsmtp' (GID 9999) ...
Adding new user 'vsmtp' (UID 9999) with group 'vsmtp' ...
Not creating home directory '/home/vsmtp'.
```

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

```shell
sudo mkdir /etc/vsmtp /etc/vsmtp/rules /etc/vsmtp/certs /var/log/vsmtp /var/spool/vsmtp
sudo chown -R vsmtp:vsmtp /var/log/vsmtp /etc/vsmtp/* /var/spool/vsmtp
```

Copy the vsmtp binaries and the config files.

```shell
sudo cp ./target/release/vsmtp /usr/sbin/
sudo cp -p ./config/vsmtp.default.toml /etc/vsmtp/vsmtp.toml
```

## MTA service

### Check and disable current MTA

Check if you have a mail transfer agent service running and disable it. The example below is related to a Postfix service running on port 25.

```shell
$ sudo ss -ltpn | grep ":25"
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

&#9758; | Depending on Linux distributions, instead of `ss` command you may have to use `netstat -ltpn`

### Adding vSMTP as a systemd service

 &#9758; | The vsmtp user must have the rights to bind to ports <1024. Version 0.10 will bring a mechanism allowing vSMTP to drop privileges at startup.

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
