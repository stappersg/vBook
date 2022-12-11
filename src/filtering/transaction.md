# Transaction context

As described in the [`Configuring vSMTP`](../get-started/config-file-struct.md) chapter, sub-domains handled by the configuration of vSMTP have three filtering entry-points: `incoming`, `outgoing` and `internal`.

```diff
/etc/vsmtp
  ┣ vsmtp.vsl
  ┣ conf.d/
  ┃     ┗ config.vsl
  ┣ domain-available/
+ ┃     ┗ example.com
+ ┃         ┣ incoming.vsl
+ ┃         ┣ outgoing.vsl
+ ┃         ┗ internal.vsl
+ ┣ domain-enabled/
+ ┃     ┣ incoming.vsl
+ ┃     ┗ example.com -> ...
```

Here is a diagram of which entry-points are executed following the transaction pipeline.

![Sub-domain Hierarchy](../assets/uml/sub-domain-hierarchy.svg)
<p class="ann"> Rules execution order following the transaction context </p>

## Root Incoming ⬜

The root `incoming.vsl` script is used to filter incoming transaction at the `connect`, `helo` and `authenticate` stages. The rules contained in those stages are applied to ALL incoming transactions.

This script also run rules under the `mail` stage when an incoming sender domain is not handled by the configuration.

Finally, if the sender's domain is not handled by the configuration, and that the domain of recipients is not as well, rules defined in the `rcpt` stage contained in the root `incoming.vsl` are also called. You should, by default, deny the transaction at this stage since it probably is a relay tentative.

```js
#{
  rcpt: [
    rule "deny relay" || deny(),
  ]
}
```
<p class="ann"> anti-relaying using rules in `incoming.vsl` </p>

> If this file is not present in the rule directory, it will deny all transactions by default.

## Incoming 🟨

The `incoming.vsl` script is run if the sender domain is not handled by the configuration, but domains from recipients are.

```sh
MAIL FROM: <john.doe@unknown.com> # We don't have a `unknown.com` folder, this is an incoming message.
RCPT TO:   <foo@example.com>      # `example.com` is handled, we run `incoming.vsl`.
RCPT TO:   <bar@example.com>      # Same as above.
```

If any recipient domain in this context is not handled by the configuration, then `fallback.vsl` is called.

```sh
MAIL FROM: <john.doe@unknown.com> # We don't have a `unknown.com` folder, this is an incoming message.
RCPT TO:   <foo@example.com>      # `example.com` is handled, we run `example.com/incoming.vsl`.
RCPT TO:   <bar@anonymous.com>    # We don't have a `unknown.com` folder, the root `incoming.vsl` is used.
```

A client should not mix up multiple recipient domains when sending a message to the server. This is why the root incoming script is called when this happens. Once again, if `incoming.vsl` is not defined, the transaction will be denied by default.

## Outgoing 🟪

The `outgoing.vsl` script is run if the sender domain is handled by the configuration, but recipients are not.

```sh
MAIL FROM: <john.doe@example.com> # `example.com` exists, this is an outgoing message.
RCPT TO:   <foo@anonymous.com>    # We don't have a `anonymous.com` folder, `outgoing.vsl` is used.
RCPT TO:   <bar@anonymous.com>    # Same as above.
```

## Internal 🟩

The `internal.vsl` script is run if the sender and recipients domains are handled by the configuration and the exact same.

```sh
MAIL FROM: <john.doe@example.com> # `example.com` exists, we don't know yet about the recipient, so this is an outgoing message for now.
RCPT TO:   <foo@example.com>    # The domain is the same as the sender, `internal.vsl` is used, it becomes an internal message now.
RCPT TO:   <bar@example.com>    # Same as above.
```

## Sub domains

Root domain rules are used when a sub domain does not have any rules configured.

For example, if the configuration has rules setup for the `example.com` domain, but does not for the `dev.example.com`, if any transaction has the `dev.example.com` sub-domain, rules for `example.com` will be used.