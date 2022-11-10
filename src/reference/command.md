# Managing vSMTP from the command line

## Starting vSMTP

vSMTP is designed to run as a Unix service and is not intended to be run interactively using the command lines. However, in case of startup problems, it can be useful to run it with a minimal configuration file to check the settings. In any case, vSMTP must be started with root privileges.

```shell
$ sudo vsmtp -c /etc/vsmtp/vsmtp-minimal.vsl
2022-05-11 17:16:40.609916181 WARN  [139916115511680] server::rule_engine            $ No 'main.vsl' provided in the config, the server will deny any incoming transaction by default.
2022-05-11 17:16:40.622996178 WARN  [139915467675200] vsmtp_server::server           $ No TLS configuration provided, listening on submissions protocol (port 465) will cause issue
```

## Managing configuration

```shell
$ vsmtp --help
vsmtp 1.0.0
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

Loaded configurations can be checked using `config-diff` and `config-show` subcommands.

```shell
$ sudo vsmtp -c /etc/vsmtp/vsmtp.vsl config-show
Loading configuration at path='/etc/vsmtp/vsmtp.vsl'
Loaded configuration: {
  "server": {
    "domain": "testserver.com",
    "addr": "0.0.0.0:25",
    "addr_submission": "0.0.0.0:587",
    "addr_submissions": "0.0.0.0:465",
    "thread_count": 10
  },
  "log": {
    "file": "/var/log/vsmtp/vsmtp.log",
    "level": {
      "receiver": "INFO",
      "rules": "WARN",
      "default": "WARN",
      "resolver": "WARN"
    }
  },
 
  "reply_codes": {
    "Code214": "214 my custom help message\r\n",
    "Code220": "220 testserver.com ESMTP Service ready\r\n",
   
    ... // etc.
  }
}
```

```shell
$ sudo vsmtp -c /etc/vsmtp/vsmtp.vsl config-diff
Loading configuration at path='/etc/vsmtp/vsmtp.vsl'
 {
   "server": {
     "domain": "testserver.com",
     "addr": "0.0.0.0:25",
     "addr_submission": "0.0.0.0:587",
     "addr_submissions": "0.0.0.0:465",
-    "thread_count": 2                      // DEFAULT configuration
+    "thread_count": 10                     // CURRENT configuration
   },
   "log": {
-    "file": "./trash/log.log",             // DEFAULT configuration            
+    "file": "/var/log/vsmtp/vsmtp.log",    // CURRENT configuration
     "level": {
-      "default": "OFF"                     
+      "resolver": "WARN",                  
+      "default": "WARN",                   // etc.
+      "rules": "WARN",
+      "receiver": "INFO"
     }
   },

   "reply_codes": {
-    "Code214": "214 joining us https://viridit.com/support\r\n",
-    "Code220": "220 testserver.com Service ready\r\n",
+    "Code214": "214 my custom help message\r\n",
+    "Code220": "220 testserver.com ESMTP Service ready\r\n",

        ... // etc.
    }
 }
```

## Managing queues

Internal and user defined queues can be managed using the `vqueue` command with root privileges.

The `vqueue show` subcommand displays a summary of vSMTP queues in a Postfix qshape way. The `-c` option allows vqueue to parse queues and quarantines defined in the main configuration file.

```shell
WORKING    is at '/var/spool/vsmtp/working' : <EMPTY>

DELIVER    is at '/var/spool/vsmtp/deliver' :
                T    5   10   20   40   80  160  320  640 1280 1280+
       TOTAL    4    0    0    0    0    0    0    0    0    4    0
example1.com    1    0    0    0    0    0    0    0    0    1    0
example2.com    1    0    0    0    0    0    0    0    0    1    0
example3.com    1    0    0    0    0    0    0    0    0    1    0
example4.com    1    0    0    0    0    0    0    0    0    1    0

DEFERRED   is at '/var/spool/vsmtp/deferred' : <EMPTY>

DEAD       is at '/var/spool/vsmtp/dead' : <EMPTY>
```

## Managing messages

Like queues, messages are also managed using the `vqueue` command.

Features available in v0.10:

- vqueue msg \<msg-id\> show [json | eml] : Print the content of a message.
- vqueue msg \<msg-id\> move \<queue\> : Move a message to a queue.
- vqueue msg \<msg-id\> remove : Remove a message from disk.

Feature planned:

- vqueue msg \<msg-id\> re-run : Reintroduce a message in the delivery system (and reevaluate its status).
- User defined quarantine queues inspection.
