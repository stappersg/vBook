# SSL/TLS

Connections should be encrypted using the SSL/TLS protocol, even on a private network.
TLS can be initiated right after connect on the [address submissions](../../ref/vSL/api/var::cfg.md), or with the STARTTLS mechanism.

Add the following to the `/etc/vsmtp/conf.d/config.vsl` file:

```js
fn on_config(config) {
  // Add root TLS settings.
  config.server.tls = #{
    preempt_cipherlist: false,
    handshake_timeout: "1000ms",
    protocol_version: ["TLSv1.2", "TLSv1.3"],
    certificate: "/etc/letsencrypt/live/mta.doe-family.com/cert.pem",
    private_key: "/etc/letsencrypt/live/mta.doe-family.com/privkey.pem",
  };

  config
}
```

> vSMTP only support certificate with the X.509 format.

And edit your `.vsl` rules to add your policy:

```js
#{
  mail: [
    rule "deny unencrypted" || {
      // You can customize your policy to whitelist some ip or anything
      if is_secured() {
        next()
      } else {
        deny(code(451, "5.7.3", "Must issue a STARTTLS command first\r\n"))
      }
    }
  ]
}
```

> See the [`is_secured`][is_secured_fn_ref] reference for more details.

[is_secured_fn_ref]: ../../ref/vSL/api/fn::global::vsl-api.md
