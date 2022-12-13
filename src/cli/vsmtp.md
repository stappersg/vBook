# vsmtp

`vsmtp` is the binary executed by the `vsmtp.service` daemon. It is usually run as a daemon but it can be used with commands to manage the configuration.

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

## Managing configuration

Loaded configurations can be checked using the `config-diff` and `config-show` commands.

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

```diff
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