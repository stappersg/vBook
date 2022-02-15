# vSMTP 



### Starting vSMTP from the command line

vSMTP was designed to run as a Unix service and is not intended to be run interactively from the command line. However, in case of startup problems, it can be useful to run it with a minimal configuration file to check the settings. In any case, vSMTP must be started with root privileges.

```shell
$ sudo vsmtp -c /etc/vsmtp/vsmtp-minimal.toml
Loading with configuration: '/etc/vsmtp/vsmtp-minimal.toml'
2022-02-05 15:05:09 WARN  140000927181184 (line:51 ) $ Listening on: [0.0.0.0:25, 0.0.0.0:587, 0.0.0.0:465]
```

### Managing configuration from the command line



### Managing queues from the command line

Theses features will be available from releases 0.10.x.
