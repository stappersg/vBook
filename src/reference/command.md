## Starting vSMTP with a command line

vSMTP is not intended to be started on a command line. 

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

However in case of startup issues it may be interesting to run with a minimal configuration file to check the parameters.

In any case, vSMTP must be started with root privileges.

```shell
$ sudo vsmtp -c /etc/vsmtp/vsmtp.toml
Loading with configuration: '/etc/vsmtp/vsmtp.toml'
2022-02-04 18:07:44 WARN  140079603337600 (line:51 ) $ Listening on: [0.0.0.0:25, 0.0.0.0:587, 0.0.0.0:465]
```

