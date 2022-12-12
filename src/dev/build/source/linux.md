# Linux installation

The installation described below was performed on an Ubuntu Server 20.04. Slight changes may be needed for other distributions.

## Install Rust language

See the official website <https://www.rust-lang.org/tools/install>

## Check dependencies

vSMTP requires the `libc` libraries and the GCC compiler/linker.
On a Debian system, they are contained in the `build-essential` package.

The authentication is provided by the [Cyrus sasl](https://www.cyrusimap.org/sasl) binary package.

```shell
sudo apt update
sudo apt install    \
  pkg-config        \
  build-essential   \
  sasl2-bin         \
```
<p class="ann"> Install vSMTP's dependencies </p>

## vSMTP compilation

`cargo` (Rust package manager) downloads all required dependencies and compile the source code in conformance to the current environment.

```shell
$> cargo build --workspace --release
[...]
$> cargo run -- --help
vsmtp 1.4
Team viridIT <https://viridit.com/>
Next-gen MTA. Secured, Faster and Greener

USAGE:
    vsmtp [OPTIONS] [SUBCOMMAND]

OPTIONS:
    -c, --config <CONFIG>      Path of the vSMTP configuration file ("vsl" format)
    -h, --help                 Print help information
    -n, --no-daemon            Do not run the program as a daemon
    -t, --timeout <TIMEOUT>    Make the server stop after a delay (human readable format)
    -V, --version              Print version information

SUBCOMMANDS:
    config-diff    Show the difference between the loaded config and the default one
    config-show    Show the loaded config (as serialized json format)
    help           Print this message or the help of the given subcommand(s)
```
<p class="ann"> Building and running the source code using `cargo` </p>

By default Rust/Cargo use static linking to compile. All libraries required are compiled into the executable, allowing vSMTP to be a standalone application.

## Configure the Operating System for vSMTP

For security purpose, vSMTP should run using a dedicated account with minimum privileges.

```shell
$ sudo adduser --system --shell /usr/sbin/nologin --no-create-home \
    --uid 9999 --group --disabled-password --disabled-login vsmtp
```
<p class="ann"> Create a user to run vSMTP </p>

```shell
Adding system user 'vsmtp' (UID 9999) ...
Adding new group 'vsmtp' (GID 9999) ...
Adding new user 'vsmtp' (UID 9999) with group 'vsmtp' ...
Not creating home directory '/home/vsmtp'.
```

vSMTP binaries and config files should be located in:

- /usr/sbin/ : binaries
- /etc/vsmtp/
  - /etc/vsmtp/vsmtp.vsl : default configuration file
  - /etc/vsmtp/rules/ : rules
  - /etc/vsmtp/certs/ : certificates
- /var/spool/vsmtp/ : internal queues
- /var/log/
  - /var/log/vsmtp.log/ : internal logs and trace
  - /var/log/mail.log and mail.err : syslog
- /home/~user/Maildir : local IMAP delivery

These default locations may be changed in the `/etc/vsmtp/vsmtp.vsl` configuration file which is called by the service startup `/etc/systemd/system/vsmtp.service` file.

```shell
sudo mkdir /etc/vsmtp /etc/vsmtp/rules /etc/vsmtp/certs /var/log/vsmtp /var/spool/vsmtp
sudo cp ./target/release/vsmtp /usr/sbin/
sudo cp ./target/release/vqueue /usr/sbin/
```
<p class="ann"> Create vSMTP directories </p>

A minimal vsmtp.vsl configuration file that matches vsmtp version (i.e. 1.0.0) must be created.

```shell
cat > /etc/vsmtp/vsmtp.vsl <<EOF
import "conf.d/config.vsl" as cfg;
let config = cfg::config;
config.version_requirement = ">=1.0.0";
EOF
```
<p class="ann"> Create a minimal configuration file </p>

```shell
sudo chown -R vsmtp:vsmtp /var/log/vsmtp /etc/vsmtp/* /var/spool/vsmtp
```
<p class="ann"> Grant rights to vSMTP files and directories </p>

If required, add private key and certificate to `/etc/vsmtp/certs` and grant reading rights to the vsmtp user.

## Configuring the MTA service

### Check and disable current MTA

Check if you have a mail transfer agent service running and disable it.

```shell
$ sudo ss -ltpn | grep ":25"
tcp        0      0 127.0.0.1:25              127.0.0.1:*               LISTEN      39423/master
```

```shell
$ sudo systemctl status postfix
● postfix.service - Postfix Mail Transport Agent
     Loaded: loaded (/lib/systemd/system/postfix.service; enabled; vendor preset: enabled)
     Active: active (exited) since Fri 2021-12-10 11:10:58 CET; 5min ago
    Process: 39426 ExecStart=/bin/true (code=exited, status=0/SUCCESS)
   Main PID: 39426 (code=exited, status=0/SUCCESS)
```

```shell
$ sudo systemctl stop postfix
$ sudo systemctl disable postfix
Synchronizing state of postfix.service with SysV service script with /lib/systemd/systemd-sysv-install.
Executing: /lib/systemd/systemd-sysv-install disable postfix
Removed /etc/systemd/system/multi-user.target.wants/postfix.service.
```
<p class="ann"> Disabling a postfix instance that was running on port 25 </p>

&#9758; | Depending on Linux distributions, instead of `ss` command you may have to use `netstat -ltpn`

### Add vSMTP as a systemd service

Copy the daemon configuration file in `/etc/systemd/system`.

```shell
sudo cp ./tools/install/deb/vsmtp.service /etc/systemd/system/vsmtp.service
```

Please note that vSMTP drops privileges at startup. The service type must be set to `forking`. 

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
             └─2164 /usr/sbin/vsmtp -c /etc/vsmtp/vsmtp.vsl

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
