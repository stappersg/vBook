# Filtering with the Sender Policy Framework

A new DNS record is added into the `doe-family.com` DNS zone. It declares that only the server specified in the MX record is allowed to send messages on behalf of Doe's family.

```shell
doe-family.com.          TXT "v=spf1 +mx -all"
```

For incoming messages, SPF is configured to check that the sending host is authorized to use the `doe-family.com` according to published SPF policy. Rules are executed at the `mail` stage.

Edit the `/etc/vsmtp/domain-enabled/incoming.vsl` file and add the following rule.
```js
#{
  mail: [
    rule "check spf" || check_spf("both", "soft"),
  ]
}
```
<p style="text-align: center;"> <i>Preventing spams using SPF</i> </p>

> Check out the [Security module](/src/reference/vSL/api/Security.md) for more details on the `check_spf` function.