# Linux installation

The installation described above was performed on an Ubuntu Server 20.04. There may be slight changes to apply for other distributions.

## Install Rust language

Follow the instruction from the official website <https://www.rust-lang.org/tools/install>

## Check dependencies

vSMTP requires `libc` libraries and GCC compiler/linker.
On a Debian system these can be installed through the `build-essential` package.

The Transport Layer Security protocol (TLS) is provided by [OpenSSL development libraries](https://www.openssl.org).
The Debian package is libssl-dev package.

The authentication is provided by the [GNU `gsasl`](https://www.gnu.org/software/gsasl) and [Cyrus `sasl`](https://www.cyrusimap.org/sasl) libraries.

`libclang` frontend is also required.

```shell
sudo apt update
sudo apt install
  pkg-config
  build-essential
  libssl-dev
  libgsasl7-dev
  libsasl2-2
  sasl2-bin
  libclang-dev
```

## vSMTP compilation

`cargo` (Rust package manager) will download all required dependencies and compile the source code in accordance with your environment.

```shell
$> cargo build
[...]
$> cargo run -- --help
vsmtp 1.1.3
Team viridIT <https://viridit.com/>
Next-gen MTA. Secured, Faster and Greener

USAGE:
    vsmtp [OPTIONS] [SUBCOMMAND]

OPTIONS:
    -c, --config <CONFIG>      Path of the vSMTP configuration file (toml format)
    -h, --help                 Print help information
    -n, --no-daemon            Do not run the program as a daemon
    -t, --timeout <TIMEOUT>    Make the server stop after a delay (human readable format)
    -V, --version              Print version information

SUBCOMMANDS:
    config-diff    Show the difference between the loaded config and the default one
    config-show    Show the loaded config (as serialized json format)
    help           Print this message or the help of the given subcommand(s)
```

By default Rust/Cargo use static linking to compile - all libraries required are compiled into the executable - allowing vSMTP to be a standalone application.

## Configure the Operating System for vSMTP

For security purpose, vSMTP should run using a dedicated account with minimal privileges.

```shell
$ sudo adduser --system --shell /usr/sbin/nologin --no-create-home \
    --uid 9999 --group --disabled-password --disabled-login vsmtp
```

```shell
Adding system user 'vsmtp' (UID 9999) ...
Adding new group 'vsmtp' (GID 9999) ...
Adding new user 'vsmtp' (UID 9999) with group 'vsmtp' ...
Not creating home directory '/home/vsmtp'.
```

vSMTP binaries and config files should be located in:

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
sudo cp ./target/release/vsmtp /usr/sbin/
sudo cp ./target/release/vqueue /usr/sbin/
```

Create a minimal vsmtp.toml configuration file that matches vsmtp version (i.e. 1.0.0)

```shell
sudo bash -c 'echo "version_requirement = \">=1.0.0\"" > /etc/vsmtp/vsmtp.toml'
```

Grant rights to files and folders.

```shell
sudo chown -R vsmtp:vsmtp /var/log/vsmtp /etc/vsmtp/* /var/spool/vsmtp
```

If required, do not forget to add your private key and certificate to /etc/vsmtp/certs and allow vsmtp user to read them.

## Configuring the MTA service

### Check and disable current MTA

Check if you have a mail transfer agent service running and disable it. The example below is related to a Postfix service running on port 25.

```shell
sudo ss -ltpn | grep ":25"
```

```shell
tcp        0      0 127.0.0.1:25              127.0.0.1:*               LISTEN      39423/master
```

```shell
sudo systemctl status postfix
```

```shell
● postfix.service - Postfix Mail Transport Agent
     Loaded: loaded (/lib/systemd/system/postfix.service; enabled; vendor preset: enabled)
     Active: active (exited) since Fri 2021-12-10 11:10:58 CET; 5min ago
    Process: 39426 ExecStart=/bin/true (code=exited, status=0/SUCCESS)
   Main PID: 39426 (code=exited, status=0/SUCCESS)
```

```shell
sudo systemctl stop postfix
sudo systemctl disable postfix
```

```shell
Synchronizing state of postfix.service with SysV service script with /lib/systemd/systemd-sysv-install.
Executing: /lib/systemd/systemd-sysv-install disable postfix
Removed /etc/systemd/system/multi-user.target.wants/postfix.service.
```

&#9758; | Depending on Linux distributions, instead of `ss` command you may have to use `netstat -ltpn`

### Add vSMTP as a systemd service

Copy the daemon configuration file to /etc/systemd/system.

```shell
sudo cp ./tools/install/deb/vsmtp.service /etc/systemd/system/vsmtp.service
```

Please note that vSMTP comes with a mechanism that drop privileges at startup. The service type must be set to `forking`.

> Do not modify this file unless you know what you are doing.

### Enable and activate vSMTP service

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

```

### Check that vSMTP is working properly

```shell
$ ss -ltpn | grep vsmtp
State    Recv-Q   Send-Q     Local Address:Port     Peer Address:Port   Process
LISTEN   0        128        127.0.0.1:587           127.0.0.1:*       users:(("vsmtp",pid=2127,fd=5))
LISTEN   0        128        127.0.0.1:465           127.0.0.1:*       users:(("vsmtp",pid=2127,fd=6))
LISTEN   0        128        127.0.0.1:25            127.0.0.1:*       users:(("vsmtp",pid=2127,fd=4))

$ nc -C localhost 25
220 mydomain.com Service ready
451 Timeout - closing connection.
```
