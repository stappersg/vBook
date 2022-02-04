## Configuring the vSMTP service

The vSMTP service (network, default directories, tls, etc.) can be configured by modifying /etc/vsmtp/vsmtp.toml file.
Please refer to the documentation for further details.
 
&#9758; | vSMTP service must be restarted to apply changes.

## Configuring SMTP filtering

SMTP filtering is performed by the rule engine. The end user can interact and modify the behavior of vSMTP by adding rules in the .vSL configuration files.

All .vSL files in the "rules" folder are scanned alphabetically and injected into the rules engine.

If there is no vSL file, the server will accept all incoming and outgoing mails, as well as domain forwarding.
For obvious security reasons, this configuration should not be deployed on a server connected directly to the Internet.

Please refer to the examples in the vSMTP repository and read the [vSMTP scripting language] for detailed information.

[vSMTP scripting language]: https://github.com/viridIT/vSMTP/wiki/vSMTP-Scripting-Language-vSL

&#9758; vSMTP service must be restarted to apply changes.




## Examples ....

### Personnal MTA/MDA

### Remote office

### Large company MTA

