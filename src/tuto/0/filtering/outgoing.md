# Outgoing messages

`doe-family.com/outgoing.vsl` is run when the sender of the domain is `doe-family.com` and that recipients domains are not `doe-family.com`.

Here, a member of Doe's family is sending an email to someone else. We just have to verify that the sender is legitimate by asking the client to authenticate itself to vSMTP. If the authentication fails, this probably means that a spammer tried to use our server as a relay. The `auth::unix_user()` function automatically denies the transaction if the authentication failed.

```
#{
  authenticate: [
    rule "sasl authentication" || auth::unix_user(),
  ],

  mail: [
    rule "deny unauthenticated" || {
      if auth::is_authenticated() {
        state::next()
      } else {
        state::deny(code(530, "5.7.0", "Authentication required\r\n"))
      }
    }
  ]
}
```

<p class="ann"> /etc/vsmtp/domain-available/doe-family.com/outgoing.vsl </p>

> ⚠️ The `auth::unix_user` function uses the `testsaslauthd` program under the hood, itself calling the `saslauthd` daemon.
> Make sure to install the [Cyrus sasl binary package](https://www.cyrusimap.org/sasl/) for the targeted distribution and configure the `saslauthd` daemon with `MECHANISM="shadow"` in `/etc/default/saslauthd`.

> See the [`auth::is_authenticated`][auth_mod] and [`auth::unix_user`][auth_mod] reference for more details.

[auth_mod]: ./../../../ref/vSL/api/fn::global::auth.md
