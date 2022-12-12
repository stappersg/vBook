# Filtering with DKIM

`DKIM` is an open standard for email authentication used to check the integrity of the content of an email. A signature header is added to the messages. This signature is secured by a key pair (private/public).

We will configure these rules:

- If the sender is an account from Doe's family, add DKIM signature to the message.
- If the recipient is an account from Doe's family, verify DKIM signatures.

## Add a DKIM record

A new DNS record is added into the `doe-family.com` DNS zone. It declares the public key usable to verify the messages.

> TODO: add an example.

## Configure vSMTP for DKIM

Add the following to the `on_config` function body in the `/etc/vsmtp/conf.d/config.vsl` file:

```rust,ignore
config.server.dkim.private_key = ["/path/to/private-key"];
```

## Add signatures

The `dkim_sign` function is used to sign your email. Use it in the `postq` stage like so:

```rust,ignore
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

<p class="ann"> /etc/vsmtp/domain-available/doe-family.com/outgoing.vsl </p>

> See the [`dkim_sign`][sign_dkim_fn_ref] reference for more details.

## Verify signatures

```rust,ignore
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

<p class="ann"> /etc/vsmtp/domain-available/doe-family.com/incoming.vsl </p>

> See the [`verify_dkim`][verify_dkim_fn_ref] reference for more details.

[verify_dkim_fn_ref]: ../../ref/vSL/api/fn::global::dkim.md
[sign_dkim_fn_ref]: ../../ref/vSL/api/fn::global::dkim.md
