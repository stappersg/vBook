## 

### Starting vSMTP from the command line

vSMTP was designed to run as a Unix service and is not intended to be run interactively from the command line. However, in case of startup problems, it can be useful to run it with a minimal configuration file to check the settings.

```shell
$ vsmtp --help
vsmtp 0.8.5
Team viridIT <https://viridit.com/>
vSMTP : the next-gen MTA. Secured, Faster and Greener

USAGE:
    vsmtp --config <CONFIG>

OPTIONS:
    -c, --config <CONFIG>
    -h, --help               Print help information
    -V, --version            Print version information

```

In any case, vSMTP must be started with root privileges.

```shell
$ sudo vsmtp -c /etc/vsmtp/vsmtp.toml
Loading with configuration: '/etc/vsmtp/vsmtp.toml'
2022-02-05 15:05:09 ERROR 140000927181184 (line:58 ) $ failed to get certificates: No such file or directory (os error 2)
2022-02-05 15:05:09 ERROR 140000927181184 (line:129) $ failed to get certificates: No such file or directory (os error 2)
2022-02-05 15:05:09 WARN  140000927181184 (line:51 ) $ Listening on: [0.0.0.0:25, 0.0.0.0:587, 0.0.0.0:465]
```

### Managing queues from the command line

Theses features will be available from releases 0.10.x.
