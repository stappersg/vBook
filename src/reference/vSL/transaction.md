# Transaction context

As described in the [`Configuring vSMTP`](/src/get-started/config-file-struct.md) chapter, sub-domains handled by the configuration of vSMTP have three filtering entry-points: `incoming`, `outgoing` and `internal`.

```diff
/etc/vsmtp
  ┣ vsmtp.vsl
  ┣ conf.d/
  ┃     ┗ config.vsl
  ┗ domain-available/
          ┣ main.vsl
          ┣ fallback.vsl
          ┗ example.com
+              ┣ incoming.vsl
+              ┣ outgoing.vsl
+              ┗ internal.vsl
```

## Incoming

The `incoming.vsl` script is run if the sender domain is not handled by the configuration, but domains from recipients are.

Thus:
```sh
MAIL FROM: <john.doe@unknown.com> # We don't have a `unknown.com` folder, this is an incoming message.
RCPT TO:   <foo@example.com>      # `example.com` is handled, we run `incoming.vsl`.
RCPT TO:   <bar@example.com>      # Same as above.
```

If any recipient domain in this context is not handled by the configuration, then `fallback.vsl` is called.

Thus:
```sh
MAIL FROM: <john.doe@unknown.com> # We don't have a `unknown.com` folder, this is an incoming message.
RCPT TO:   <foo@example.com>      # `example.com` is handled, we run `incoming.vsl`.
RCPT TO:   <bar@anonymous.com>    # We don't have a `unknown.com` folder, `fallback.vsl` is used.
```

A client should not mix up multiple recipient domains when sending a message to the server. This is why the fallback script is called when this happens. Once again, if `fallback.vsl` is not defined, the transaction will be denied by default.

## Outgoing

The `outgoing.vsl` script is run if the sender domain is handled by the configuration, but recipients are not.

Thus:
```sh
MAIL FROM: <john.doe@example.com> # `example.com` exists, this is an outgoing message.
RCPT TO:   <foo@anonymous.com>    # We don't have a `anonymous.com` folder, `outgoing.vsl` is used.
RCPT TO:   <bar@anonymous.com>    # Same as above.
```

## Internal

The `internal.vsl` script is run if the sender and recipients domains are handled by the configuration and the exact same.

Thus:
```sh
MAIL FROM: <john.doe@example.com> # `example.com` exists, we don't know yet about the recipient, so this is an outgoing message.
RCPT TO:   <foo@example.com>    # The domain is the same as the sender, `internal.vsl` is used.
RCPT TO:   <bar@example.com>    # Same as above.
```

## Sub-domain specific configuration

It is possible to add a specific configuration for each sub domain. 

```diff
/etc/vsmtp
  ┣ vsmtp.vsl
  ┣ conf.d/
  ┃     ┣ config.vsl
  ┃     ┣ interfaces.vsl
  ┃     ┗ app.vsl
  ┗ domain-available/
          ┣ main.vsl
          ┣ fallback.vsl
          ┗ example.com
+             ┣ config.vsl
              ┣ incoming.vsl
              ┣ outgoing.vsl
              ┗ internal.vsl
```

The `config.vsl` under a sub domain must contain the following statement:

```rust
fn on_domain_config(config) {
  config
}
```

As the root `config.vsl` file, it contains a callback used to configure the sub domain. You can configure TLS, DKIM and DNS per sub-domain using this script.

For example:
```rust
fn on_domain_config(config) {
  config.tls = #{
    protocol_version: ["TLSv1.2", "TLSv1.3"],
    certificate: "/etc/vsmtp/certs/cert.pem",
    private_key: "/etc/vsmtp/certs/privkey.pem",
  };

  config.dkim = #{
    private_key: "/etc/vsmtp/certs/example.dkim.key",
  };

  config.server.dns.type = "system";

  config
}
```

If this script is not present in a subdomain, configuration from the root `config.vsl` file is used instead.