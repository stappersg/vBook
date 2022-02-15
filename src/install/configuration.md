# Configuring the vSMTP service

The vSMTP service (network, default directories, tls, etc.) can be configured by modifying /etc/vsmtp/vsmtp.toml file. Please refer to the documentation for further details.
 
&#9758; | vSMTP service must be restarted to apply changes.

## Add a SSL key

Irure aute fugiat aute adipisicing. Eiusmod do proident nisi qui adipisicing in aliqua aliqua ea do fugiat velit do est. Sunt laborum voluptate exercitation occaecat excepteur ad amet incididunt consectetur cillum proident dolor. Ut aliqua labore fugiat irure amet non duis eiusmod. Est esse aliquip aliqua amet ipsum. Sit consectetur minim ex consequat commodo consectetur irure minim anim. Reprehenderit irure eu consectetur irure in anim velit mollit incididunt consectetur.

```shell
openssl genrsa -out private.key 4096
openssl req -key private.key -new -x509 -out certificate.crt
```

Irure amet duis reprehenderit fugiat ullamco quis magna dolore ullamco ea ut sint Lorem mollit. Labore consequat quis incididunt officia consequat. Tempor veniam aliquip consequat aute excepteur consectetur et nostrud amet do ipsum.

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

Incididunt voluptate commodo aliquip do. Do ea est sint labore nulla mollit pariatur. Nostrud sunt ex laboris velit id sit adipisicing. Reprehenderit incididunt qui proident Lorem magna commodo. Dolore enim veniam aliquip consectetur irure tempor dolor proident laboris sunt qui labore excepteur. Est ad nostrud labore sunt Lorem pariatur consectetur ipsum. Incididunt mollit sint reprehenderit non ad dolore aliqua occaecat consectetur. Aliquip aute est elit reprehenderit esse reprehenderit. Consectetur ullamco eiusmod dolor irure excepteur. Esse labore elit in esse ea nostrud eiusmod. Labore amet culpa cillum incididunt consectetur eu aliqua commodo velit exercitation ut deserunt elit proident.

## Minimal configuration file

Culpa laboris dolore sit sit non. Laboris adipisicing aliquip ad eu cillum veniam mollit magna fugiat Lorem dolor nostrud laboris duis. Aliquip ullamco excepteur proident mollit ut ad non ea cupidatat.