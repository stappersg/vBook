# vqueue

`vqueue` is a cli utility that is used to inspect and manage vSMTP's queues.

## Managing queues

Internal and user defined queues can be managed using the `vqueue` command with root privileges.

The `vqueue show` subcommand displays a summary of vSMTP queues in a Postfix qshape way. The `-c` option allows vqueue to parse queues and quarantines defined in the configuration.

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
