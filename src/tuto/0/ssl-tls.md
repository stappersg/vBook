# SSL/TLS

> ℹ️ To use SMTPS, you will need a valid TLS certificate and a private key for your server.
>
> vSMTP support X.509 certificates and RSA/PKCS8/EC keys stored in `.pem` files.

TLS can be initiated right after connect on the [address submissions],
or with the `STARTTLS` mechanism.

```rust,ignore
fn on_config(config) {
  // Add root TLS settings.
  config.server.tls = #{
    preempt_cipherlist: false,
    handshake_timeout: "1000ms",
    protocol_version: ["TLSv1.2", "TLSv1.3"],
  };

  config
}
```

<p class="ann"> Adding tls configuration to `/etc/vsmtp/conf.d/config.vsl` </p>

## Policy

Rules can then be added to filter out unsecure transactions.

```
#{
  mail: [
    rule "deny unencrypted" || {
      // It is possible to customize the policy to whitelist some ip for example.
      if ctx::is_secured() {
        state::next()
      } else {
        state::deny(code(451, "5.7.3", "Must issue a STARTTLS command first\r\n"))
      }
    }
  ]
}
```

<p class="ann"> Adding rules to check if the transaction is secured in `/etc/vsmtp/filter.vsl` </p>

> See the [`ctx::is_secured`][is_secured_fn_ref] reference for more details.

## Certificate / SNI

You can host multiple domains on the same server. The certificate resolution of the server is based
on the [SNI] extension.

By default, [SNI] is required. Meaning both these commands will produce an error.

```sh
openssl s_client -starttls smtp -crlf -connect 192.168.1.254:25
openssl s_client -crlf -connect 192.168.1.254:465
```

To support TLS for a virtual server, add those lines to your configuration.

```rust,ignore
fn on_domain_config(config) {
  config.tls = #{
    certificate: "/etc/vsmtp/certs/fullchain.pem",
    private_key: "/etc/vsmtp/certs/privkey.pem",
  };

  config
}
```

<p class="ann"> `/etc/vsmtp/domain-available/example.com/config.vsl` </p>

You can then test the connection with the following command:

```sh
openssl s_client -starttls smtp -crlf -connect 192.168.1.254:25 -servername example.com
openssl s_client -crlf -connect 192.168.1.254:465 -servername example.com
```

## Default domain

You can specify which domain will be used by default when no [SNI] is provided.

```rust,ignore
fn on_config(config) {
  // ...

  config.server.tls = #{
    // ...
    certificate: "/etc/vsmtp/certs/fullchain.pem",
    private_key: "/etc/vsmtp/certs/privkey.pem",
  };

  config
}
```

<p class="ann"> Set a default domain `/etc/vsmtp/conf.d/config.vsl` </p>

These command will now work.

```sh
openssl s_client -starttls smtp -crlf -connect 192.168.1.254:25
openssl s_client -crlf -connect 192.168.1.254:465
```

[address submissions]: ../../ref/vSL/api/var::cfg.md
[is_secured_fn_ref]: ../../ref/vSL/api/fn::global::ctx.md
[SNI]: https://en.wikipedia.org/wiki/Server_Name_Indication
