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

The path to private keys for DKIM can be specified in the `/etc/vsmtp/conf.d/config.vsl` script:

```rust,ignore
fn on_config(config) {
  config.server.dkim.private_key = ["/path/to/private-key-1", "/path/to/private-key-2", ...];
  config
}
```
<p class="ann"> Configuring DKIM keys </p>

It is also possible to configure keys per domain.

```rust,ignore
fn on_domain_config(config) {
  config.dkim.private_key = ["/path/to/private-key-1", "/path/to/private-key-2", ...];
  config
}
```
<p class="ann"> Configuring DKIM keys for a specific domain (f.e. example.com)</p>

> If a key cannot be found for a specific domain, the root dkim keys are used instead.

## Add signatures

Sign an email using the [`dkim::sign`][sign_dkim_fn_ref] function for outgoing emails.

```
#{
  postq: [
    action "sign dkim" || {
      // Iterate over all the private keys defined for the server 'example.com'

      for key in dkim::get_private_keys("example.com") {
        dkim::sign(
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

Verify DKIM signatures of incoming emails by calling the [`dkim::verify`][verify_dkim_fn_ref] function.

```ignore
#{
  // ... previous rules ...

  postq: [
    rule "verify DKIM signatures" || {
      if dkim::verify().status == "pass" {
        state::accept()
      } else {
        state::deny()
      }
    }
  ],
}
```

<p class="ann"> /etc/vsmtp/domain-available/example.com/incoming.vsl </p>

> To check if DKIM is working correctly, check out [this site](https://appmaildev.com/en/dkim).

[verify_dkim_fn_ref]: ../../ref/vSL/api/fn::global::dkim.md
[sign_dkim_fn_ref]: ../../ref/vSL/api/fn::global::dkim.md
