# Filtering with DKIM

A new DNS record is added into the `doe-family.com` DNS zone. It declares the public key usable to verify the messages.

> TODO: add an example.

We will configure these rules:

- If the sender is an account from Doe's family, add DKIM signature to the message.
- If the recipient is an account from Doe's family, verify DKIM signatures.

## Configure vSMTP for DKIM

Add the following to the `on_config` function body in the `/etc/vsmtp/conf.d/config.vsl` file:

```js
config.server.dkim.private_key = "/path/to/private-key";
```

## Add signatures

The `dkim_sign` function is used to sign your email. Use it in the `postq` stage like so:
```js
#{
  // ... previous rules ...

  postq: [
    action "sign dkim" || sign_dkim(
      "2022-09", // Selector of the DNS record.
      ["From", "To", "Date", "Subject", "From"], // Headers to sign with.
      "simple/relaxed" // Canonicalization algorithm to use.
    ),
  ],
}
```
<p style="text-align: center;"> <i>/etc/vsmtp/domain-available/doe-family.com/outgoing.vsl</i> </p>

> Check out the [Security module](/src/reference/vSL/api/Security.md) for more details on the `dkim_sign` function.

## Verify signatures

The `verify_dkim` function is used check if the given signature are valid. Use it in the `postq` stage like so:

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
<p style="text-align: center;"> <i>/etc/vsmtp/domain-available/doe-family.com/incoming.vsl</i> </p>

> Check out the [Security module](/src/reference/vSL/api/Security.md) for more details on the `verify_dkim` function.