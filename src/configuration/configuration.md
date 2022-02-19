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

The main.vsl file in the "rules" folder is injected into the rules engine. It is the entry point for a custom configuration.

If there is no vSL file, the server will accept all incoming and outgoing mails, as well as domain forwarding.
For obvious security reasons, this configuration should not be deployed on a server connected directly to the Internet.

Please refer to the examples in the vSMTP repository and read the [vSMTP scripting language] for detailed information.

[vSMTP scripting language]: https://github.com/viridIT/vSMTP/wiki/vSMTP-Scripting-Language-vSL

&#9758; | vSMTP service must be restarted to apply changes.

