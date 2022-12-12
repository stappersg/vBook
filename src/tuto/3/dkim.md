# Using DKIM

DKIM is an open standard for email authentication used to check the integrity of the content of an email.
In this tutorial, we will set up DKIM by:

- Adding DNS TXT records for DKIM.
- Generate keys to encrypt and verify emails.
- Add filtering for incoming and outgoing emails using DKIM.

We will use the `example.com` domain for this example, but feel free to replace it by your own domain.

## Configure the DNS

A new DNS record is added into the `example.com` DNS zone. This record declares the public key usable to verify the messages. (See the [`What is DKIM` chapter](../../term/dkim.md) for more details)

> TODO: add command line example.

## Generate Keys

> TODO: add commands using lets encrypt.

## vSMTP root configuration

The path to a private key for DKIM can be specified in the `/etc/vsmtp/conf.d/config.vsl` script:

```rust,ignore
config.server.dkim.private_key = ["/path/to/private-key"];
```

## Add signatures

You can sign an email using the [`dkim_sign`][sign_dkim_fn_ref] function for outgoing emails.

```rust,ignore
#{
  postq: [
    action "sign dkim" || {
      // Iterate over all the private keys defined for the server 'example.com'

      for key in get_private_keys(srv(), "example.com") {
        sign_dkim(
          // Selector of the DNS record.
          "2022-09",
          // The private key associated with the public key in `{selector}._domainkey.{sdid}`
          // Or `2022-09._domainkey.example.com.` in that case
          key,
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

<p class="ann"> /etc/vsmtp/domain-available/example.com/outgoing.vsl </p>

## Verify signatures

You can verify DKIM signatures of incoming emails by calling the [`verify_dkim`][verify_dkim_fn_ref] function.

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

<p class="ann"> /etc/vsmtp/domain-available/example.com/incoming.vsl </p>

[verify_dkim_fn_ref]: ../../ref/vSL/api/fn::global::dkim.md
[sign_dkim_fn_ref]: ../../ref/vSL/api/fn::global::dkim.md
