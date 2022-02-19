# Command line 



## Starting vSMTP from the command line

vSMTP was designed to run as a Unix service and is not intended to be run interactively from the command line. However, in case of startup problems, it can be useful to run it with a minimal configuration file to check the settings. In any case, vSMTP must be started with root privileges.

```shell
$ sudo vsmtp -c /etc/vsmtp/vsmtp-minimal.toml
Loading with configuration: '/etc/vsmtp/vsmtp-minimal.toml'
2022-02-05 15:05:09 WARN  140000927181184 (line:51 ) 
Listening on: [0.0.0.0:25, 0.0.0.0:587, 0.0.0.0:465]
```

## Managing configuration from the command line

```shell
$ sudo vsmtp --help
vsmtp 0.8.6
Team viridIT <https://viridit.com/>
vSMTP : the next-gen MTA. Secured, Faster and Greener

USAGE:
    vsmtp --config <CONFIG> [SUBCOMMAND]

OPTIONS:
    -c, --config <CONFIG>
    -h, --help               Print help information
    -V, --version            Print version information

SUBCOMMANDS:
    config-diff    Show the difference between the loaded config and the default one
    config-show    Show the loaded config (as json)
    help           Print this message or the help of the given subcommand(s)
```

Loaded config can be checked using `config-diff` and `config-show` subcommands.


```json
$ sudo vsmtp -c /etc/vsmtp/vsmtp.toml config-show
Loading configuration at path='/etc/vsmtp/vsmtp.toml'
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

```json
$ sudo vsmtp -c /etc/vsmtp/vsmtp.toml config-diff
Loading configuration at path='/etc/vsmtp/vsmtp.toml'
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

## Managing queues from the command line

Theses features will be available from releases 0.10.x.
