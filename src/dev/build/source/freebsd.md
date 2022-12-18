# FreeBSD installation

The installation described above was performed on an FreeBSD 13.0 server.

## Installing Rust language

Rust port, packages and information can be found on the [freshports] website. Find more information about packages and port in the [FreeBSD handbook].

[freshports]: https://www.freshports.org/lang/rust/
[FreeBSD handbook]: https://docs.freebsd.org/en/books/handbook/

```shell
pkg install lang/rust
```

> Rust 1.60+ package is required. It may be necessary to switch to the latest ports branch. Please refer to the [freeBSD wiki].

[freeBSD wiki]: https://wiki.freebsd.org/Ports/QuarterlyBranch

## Dependencies

FreeBSD 13.x includes all required dependencies. Check that sasl is included in the used release. (See Linux dependencies)

## vSMTP compilation

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

## Configuring the Operating System for vSMTP

Create the directories and change the owner and group.

```shell
mkdir /etc/vsmtp /etc/vsmtp/rules /etc/vsmtp/certs /var/log/vsmtp /var/spool/vsmtp
cp ./target/release/vsmtp /usr/sbin/
cp ./target/release/vqueue /usr/sbin/
cp ./examples/config/minimal.vsl /etc/vsmtp/vsmtp.vsl
chown -R vsmtp:vsmtp /var/log/vsmtp /etc/vsmtp/* /var/spool/vsmtp
```

Create a minimal vsmtp.vsl configuration file that matches vsmtp version (i.e. 1.0.0)

```shell
cat > /etc/vsmtp/vsmtp.vsl <<EOF
import "conf.d/config.vsl" as cfg;
let config = cfg::config;
config.version_requirement = ">=1.0.0";
EOF
```

Grant rights to files and folders.

```shell
chmod 555 /usr/sbin/vsmtp
sudo chown -R vsmtp:vsmtp /var/log/vsmtp /etc/vsmtp/* /var/spool/vsmtp
```

If required, add private key and certificate to `/etc/vsmtp/certs` and grant reading rights to the vsmtp user.

### Disabling sendmail

Sendmail may have been disabled during FreeBSD installation. If not, add the following lines in the `/etc/rc.conf` file and reboot the system.

```shell
sendmail_enable="NO"
sendmail_submit_enable="NO"
sendmail_outbound_enable="NO"
sendmail_msp_queue_enable="NO"
```

Use sockstat command to check that sendmail is disabled.

#### Add vSMTP user:group

```shell
pw groupadd vsmtp -g 999
pw useradd vsmtp -u 999 -d /noexistent -g vsmtp -s /sbin/nologin
chown -R vsmtp:vsmtp /var/log/vsmtp /etc/vsmtp/* /var/spool/vsmtp
```

## Adding a vSMTP as a system service

vSMTP drops privileges at startup. User ACLs are no longer needed.

Please add:

- the flag `vsmtp_enable="YES" in /etc/rc.conf.
- the vsmtp script in /usr/local/etc/rc.d

```shell
cp ./tools/install/freebsd/freebsd-vsmtp.service /usr/local/etc/rc.d/vsmtp
```

```shell
#! /bin/sh

# PROVIDE: vsmtp
# REQUIRE: DAEMON
# KEYWORD: shutdown

#
# Add the following lines to /etc/rc.conf to enable vsmtp:
#
# vsmtp_enable="YES"

. /etc/rc.subr

name="vsmtp"
rcvar="${name}_enable"

load_rc_config $name

: ${vsmtp_enable:=NO}
: ${vsmtp_config:=/etc/vsmtp/vsmtp.vsl}
: ${vsmtp_flags:=--config}

command="/usr/sbin/vsmtp"
command_args="${vsmtp_config}"

run_rc_command "$1"
```

### Starting with a non privileged user

To start with an other mechanism please follow these instructions: 
- Grant the rights to the user to bind on ports <1024.
- [kernel] must be updated to support network [ACL].
- Add to these options to the KERNEL file and rebuild it.

[kernel]: https://docs.freebsd.org/en/books/handbook/kernelconfig/
[ACL]: https://docs.freebsd.org/en/books/handbook/mac/

```console
options MAC
options MAC_PORTACL
```

```shell
cd /usr/src
make buildkernel KERNCONF=MYKERNEL
make installkernel KERNCONF=MYKERNEL
```

```shell
$ sysctl security.mac
security.mac.portacl.rules:
security.mac.portacl.port_high: 1023
security.mac.portacl.autoport_exempt: 1
security.mac.portacl.suser_exempt: 1
security.mac.portacl.enabled: 1
security.mac.mmap_revocation_via_cow: 0
security.mac.mmap_revocation: 1
security.mac.labeled: 0
security.mac.max_slots: 4
security.mac.version: 4
```

```shell
$ sysctl security.mac.portacl.rules=uid:999:tcp:25,uid:999:tcp:587,uid:999:tcp:465
security.mac.portacl.rules: uid:999:tcp:25, -> uid:999:tcp:25,uid:999:tcp:587,uid:999:tcp:465
$ sysctl security.mac.portacl.rules
security.mac.portacl.rules: uid:999:tcp:25,uid:999:tcp:587,uid:999:tcp:465
$ sysctl net.inet.ip.portrange.reservedlow=0
net.inet.ip.portrange.reservedlow: 0 -> 0
$ sysctl net.inet.ip.portrange.reservedhigh=0
net.inet.ip.portrange.reservedhigh: 1023 -> 0
```

The user with uid 999 should now be authorized to bind on standard SMTP ports (25, 587, 465).
