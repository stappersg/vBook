# Outgoing messages

`doe-family.com/outgoing.vsl` is run when the sender of the domain is `doe-family.com` and that recipients domains are not `doe-family.com`.

Here, a member of Doe's family is sending an email to someone else. We just have to verify that the sender is legitimate by asking the client to authenticate itself to vSMTP. If the authentication fails, this probably means that a spammer tried to use our server as a relay. The `authenticate()` function automatically denies the transaction if the authentication failed.

```js
#{
  authenticate: [
    rule "sasl authentication" || authenticate(),
  ],
  mail: [
    rule "deny unauthenticated" || {
      if is_authenticated() {
        next()
      } else {
        deny(code(530, "5.7.0", "Authentication required\r\n"))
      }
    }
  ]
}
```

<p class="ann"> doe-family.com/outgoing.vsl </p>

> ⚠️ The `authenticate` function uses the `testsaslauthd` program under the hood, itself calling the `saslauthd` daemon.
> Make sure to install the [Cyrus sasl binary package](https://www.cyrusimap.org/sasl/)for your distribution and configure the `saslauthd` daemon with `MECHANISM="shadow"` in `/etc/default/saslauthd`.

> See the [`is_authenticated`][is_auth_fn_ref] and [`authenticate`][auth_fn_ref] reference for more details.

[auth_fn_ref]: ./../../../ref/vSL/api/fn::global::vsl-api.md
[is_auth_fn_ref]: ./../../../ref/vSL/api/fn::global::mail_context.md
