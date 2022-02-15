# Configuring the vSMTP service

The vSMTP service (network, default directories, tls, etc.) can be configured by modifying /etc/vsmtp/vsmtp.toml file. Please refer to the documentation for further details.

&#9758; | vSMTP service must be restarted to apply changes.

## Minimal configuration file

Quis excepteur et ea in aute proident tempor. Ea Lorem aliquip enim do aliqua ea enim ex et sit Lorem in sint. Do fugiat velit culpa qui mollit ullamco laboris velit veniam proident cupidatat enim amet excepteur. Elit et duis sint do exercitation velit laboris sint Lorem. Nostrud veniam et laboris deserunt officia deserunt voluptate ullamco. Exercitation velit culpa ipsum sit Lorem.

## Adding a SSL key

To start vSMTP requires a private RSA key and a certificate. The easy way to generate them is to use the `openssl` command.

&#9758; | The [OpenSSL Cookbook] covers the most frequently used OpenSSL features and commands. Thanks to its author, Ivan Ristić, a free download is available on [Feisty Duck] website.

[OpenSSL Cookbook]: https://www.feistyduck.com/books/openssl-cookbook/

```shell
openssl genrsa -out private.key 4096
openssl req -key private.key -new -x509 -out certificate.crt
```

Add these to the vSMTP `certs` directory defined in the vsmtp.toml.

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
