# Authentication

Doe's family users must be authenticated if they send messages from an external network (i.e. from a cellular net). As John decided to create Unix users, the shadow mechanism is required.

Add the following to your `/etc/vsmtp/vsmtp.toml` file:

```toml
# ...

[server.smtp.auth]
must_be_authenticated = false
enable_dangerous_mechanism_in_clair = false
```

And this rule to your `/etc/vsmtp/rules/main.vsl` file:

```js
#{
  // ... previous code ...

  authenticate: [
    rule "auth /etc/shadow" || { authenticate() }
  ],
}
```

> ⚠️ `authenticate()` function call the program `testsaslauthd` itself calling the `saslauthd` daemon.
> Make sure to configure `saslauthd` daemon with `MECHANISM="shadow"` in `/etc/default/saslauthd`.
> Future releases will bring improved vSL API.
