# Configuring the vSMTP service

## vSMTP configuration file

The vSMTP service (network, default directories, tls, etc.) can be configured by modifying the vsmtp.toml file. Its default location is /etc/vsmtp.

When starting vSMTP, the configuration file is read and entirely parsed, producing an error if the format is invalid or a field value is incorrect. The server never crashes if the configuration is loaded successfully.

The folder [examples/config](https://github.com/viridIT/vSMTP/tree/develop/examples/config) contains example of vSMTP configuration. All the field are optional and are set to their defaulted value if missing.

&#9758; | vSMTP service must be restarted to apply changes.

## Configuring SMTP filtering

SMTP filtering is performed by the rule engine. The end user can interact and modify the behavior of vSMTP by adding objects and rules in the .vSL configuration files. The main.vsl file in the "rules" folder is injected into the rules engine. It is the entry point for a custom configuration.

If there is no vSL file, the server will refuse all incoming and outgoing mails, as well as domain forwarding.

Please refer to the examples in the vSMTP repository and read the [reference guide on vSL](../reference/vSL/vsl.md) for detailed information.


&#9758; | vSMTP service must be restarted to apply changes.

