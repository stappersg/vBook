# SSL/TLS

Connections should be encrypted using the SSL/TLS protocol, even on a private network.
TLS can be initiated right after connect on the [address submissions](../../ref/vSL/api/var::cfg.md),
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

[is_secured_fn_ref]: ../../ref/vSL/api/fn::global::ctx.md

## Certificate / SNI

The certificate resolution of the server is **exclusively** based on the [SNI](https://en.wikipedia.org/wiki/Server_Name_Indication) extension. Meaning both these commands will produce an error.

```sh
openssl s_client -starttls smtp -crlf -connect 192.168.1.254:25
openssl s_client -crlf -connect 192.168.1.254:465
```

To support TLS for a virtual server, add those lines to your configuration.

```rust,ignore
fn on_domain_config(config) {
  config.tls = #{
    protocol_version: ["TLSv1.2", "TLSv1.3"],
    certificate: "/etc/vsmtp/certs/fullchain.pem",
    private_key: "/etc/vsmtp/certs/privkey.pem",
  };

  config
}
```

<p class="ann"> `/etc/vsmtp/domain-available/example.com/config.vsl` </p>

> vSMTP only support certificates with the X.509 format.

You can then test the connection with the following command:

```sh
openssl s_client -starttls smtp -crlf -connect 192.168.1.254:25 -servername example.com
openssl s_client -crlf -connect 192.168.1.254:465 -servername example.com
```
