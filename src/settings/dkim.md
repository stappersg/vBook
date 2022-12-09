# DomainKeys Identified Mail

A new DNS record is added into the desired DNS zone. This record declares the public key usable to verify the messages. (See the [DKIM chapter](../tuto/0/dkim/details.md) for more details)

> TODO: add command line example.

## Configure vSMTP for DKIM

Add the following to the `on_config` function body in the `/etc/vsmtp/conf.d/config.vsl` file:

```js
config.server.dkim.private_key = ["/path/to/private-key"];
```

## Add signatures

The `dkim_sign` function is used to sign your email. Use it in the `postq` stage like so:

```js
#{
  // ... previous rules ...

  postq: [
    action "sign dkim" || {
      // Iterate over all the private keys defined for the server 'example.com'

      for i in get_private_keys(srv(), "example.com") {
        sign_dkim(
          // Selector of the DNS record.
          "2022-09",
          // The private key associated with the public key in `{selector}._domainkey.{sdid}`
          // Or `2022-09._domainkey.example.com.` in that case
          i,
          // Headers to sign with.
          ["From", "To", "Date", "Subject", "From"],
          // Canonicalization algorithm to use.
          "simple/relaxed"
        );
      }
    }
  ],
}
```

<p style="text-align: center;"> <i>/etc/vsmtp/domain-available/example.com/outgoing.vsl</i> </p>

> See the [`dkim_sign`][sign_dkim_fn_ref] reference for more details.

## Verify signatures

```js
#{
  // ... previous rules ...

  postq: [
    rule "verify DKIM signatures" || {
      if verify_dkim().status == "pass" {
        accept()
      } else {
        deny()
      }
    }
  ],
}
```

<p style="text-align: center;"> <i>/etc/vsmtp/domain-available/example.com/incoming.vsl</i> </p>

> See the [`verify_dkim`][verify_dkim_fn_ref] reference for more details.

[verify_dkim_fn_ref]: ../ref/vSL/api/fn::global::dkim.md
[sign_dkim_fn_ref]: ../ref/vSL/api/fn::global::dkim.md
