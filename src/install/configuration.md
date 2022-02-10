# Configuring the vSMTP service

The vSMTP service (network, default directories, tls, etc.) can be configured by modifying /etc/vsmtp/vsmtp.toml file.
Please refer to the documentation for further details.
 
&#9758; | vSMTP service must be restarted to apply changes.


## ADd a key

Sint eiusmod ex laborum nisi commodo. Nostrud tempor mollit veniam consectetur officia proident enim officia. Exercitation pariatur anim proident pariatur consequat in duis eiusmod ut sint sunt. Tempor amet dolore esse incididunt eiusmod eu sunt sit. Velit mollit ullamco pariatur quis. Fugiat laborum culpa mollit veniam labore ex aute tempor.

## Security

Une clé devrait normalement être utilisée....

```shell
openssl genrsa -out private.key 4096
openssl req -key private.key -new -x509 -out certificate.crt
```

## Configuring SMTP filtering

SMTP filtering is performed by the rule engine. The end user can interact and modify the behavior of vSMTP by adding rules in the .vSL configuration files.

All .vSL files in the "rules" folder are scanned alphabetically and injected into the rules engine.

If there is no vSL file, the server will accept all incoming and outgoing mails, as well as domain forwarding.
For obvious security reasons, this configuration should not be deployed on a server connected directly to the Internet.

Please refer to the examples in the vSMTP repository and read the [vSMTP scripting language] for detailed information.

[vSMTP scripting language]: https://github.com/viridIT/vSMTP/wiki/vSMTP-Scripting-Language-vSL

&#9758; | vSMTP service must be restarted to apply changes.

## Examples ....

### Personal MTA/MDA

ISP --- FW --- MTA
         |
    Internal Network

___Firewall rules___

```shell
Public IP NAT <> MTA (192.168.1.254/32) : SMTP 25
Internal NET (192.168.0.0/24) > MTA : SMTP 25
internal NET > MTA : IMAP 110

Domain name : foo.bar
Users : john.doe@foo.bar, jane.doe@foo.bar, jimmy.doe@foo.bar, jenny.doe@foo.bar
```

___rules.vsmtp___

```rust,ignore
obj ip4 "MDA_IP" "192.168.0.1";
obj fqdn "Local_DN" "foo.bar";

obj rg4 "NET_192_168_0" "192.168.0.0/24";

obj val "SEC_LOG" "/var/log/mail/sec_log";

// User syntax is first.last
obj regex "User_Syntax" "^[a-z]+[.][a-z0-9]+";

// let Local_DN = "foo.bar";

rule rcpt "Rcpt_Antirelay" #{
    condition: (email.rcpt.domain != Local_DN) && (email.client_addr.IN(NET_192_168_0))
    on_success: { 
        LOG(`${date}:${time} : Relay attempt from : email.client_addr`, SEC_LOG); 
        DENY()
    },
    on_failure: CONTINUE()


```