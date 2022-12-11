# Filtering with DKIM

A new DNS record is added into the `doe-family.com` DNS zone. It declares the public key usable to verify the messages.

> TODO: add an example.

We will configure these rules:

- If the sender is an account from Doe's family, add DKIM signature to the message.
- If the recipient is an account from Doe's family, verify DKIM signatures.

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
      // Iterate over all the private keys defined for the server 'doe-family.com'

      for i in get_private_keys(srv(), "doe-family.com") {
        sign_dkim(
          // Selector of the DNS record.
          "2022-09",
          // The private key associated with the public key in `{selector}._domainkey.{sdid}`
          // Or `2022-09._domainkey.doe-family.com.` in that case
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

<p class="ann"> <i>/etc/vsmtp/domain-available/doe-family.com/outgoing.vsl</i> </p>

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

<p class="ann"> <i>/etc/vsmtp/domain-available/doe-family.com/incoming.vsl</i> </p>

> See the [`verify_dkim`][verify_dkim_fn_ref] reference for more details.

[verify_dkim_fn_ref]: ../../../ref/vSL/api/fn::global::dkim.md
[sign_dkim_fn_ref]: ../../../ref/vSL/api/fn::global::dkim.md
