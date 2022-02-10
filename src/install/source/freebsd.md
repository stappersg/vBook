## Installing RUST language

Rust port, packages and information can be found on [freshports] website. You can find more information about packages and port in the [FreeBSD handbook].

[freshports]: https://www.freshports.org/lang/rust/
[FreeBSD handbook]: https://docs.freebsd.org/en/books/handbook/

```shell
pkg install lang/rust
```

## Dependencies

FreeBSD 13.x comes with all required dependencies like OpenSSL.

## vSMTP compilation

```shell
git clone https://github.com/viridIT/vSMTP.git
cargo build --release
cargo run -V
```

By default Rust/Cargo use static linking to compile - all libraries required are compiled into the executable - allowing vSMTP to be a standalone application.

## Configuring the Operating System for vSMTP

For security purpose, vSMTP should run using a dedicated account with minimal privileges.

```shell

TO DO  PW ??????

$ sudo adduser --system --shell /usr/sbin/nologin --no-create-home \
    --uid 9999 --group --disabled-password --disabled-login vsmtp
Adding system user 'vsmtp' (UID 9999) ...
Adding new group 'vsmtp' (GID 9999) ...
Adding new user 'vsmtp' (UID 9999) with group 'vsmtp' ...
Not creating home directory '/home/vsmtp'.
```

Create the directories and change the owner and group.

```shell
sudo mkdir /etc/vsmtp /etc/vsmtp/rules /etc/vsmtp/certs /var/log/vsmtp /var/spool/vsmtp
sudo chown -R vsmtp:vsmtp /var/log/vsmtp /etc/vsmtp/* /var/spool/vsmtp
```

Copy the vsmtp binaries and the config files.

```shell
sudo cp ./target/release/vsmtp /usr/sbin/
sudo cp -p ./config/vsmtp.default.toml /etc/vsmtp/vsmtp.toml
```

#### Disabling sendmail

Sendmail daemon must be disabled at startup. Add the following in the /etc/rc.conf file and reboot the system.

```shell
sendmail_enable="NO"
sendmail_submit_enable="NO"
sendmail_outbound_enable="NO"
sendmail_msp_queue_enable="NO"
```

Use sockstat command to check that send mail is disabled.

```shell
# sockstat -4l
USER     COMMAND    PID   FD PROTO  LOCAL ADDRESS         FOREIGN ADDRESS
root     sshd       1053  4  tcp4   *:22                  *:*
root     syslogd    957   7  udp4   *:514                 *:*
```

#### Adding vSMTP as a FreeBSD service

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


OPTION NONE ?
SI IL FAUT INSTALL UNE CLE >>> MANDATORY ???

openssl genrsa -out privateKey.key 4096

openssl req -key privateKey.key -new -x509 -out certificate.crt
