# Filtering with the Sender Policy Framework

SPF is an authentication standard used to link a domain name and an email address. it allows email clients to verify that incoming email from a domain comes from a host authorized by the administrator of this domain.

## Add a DNS TXT record for SPF

A new DNS record is added into the `doe-family.com` DNS zone. It declares that only the server specified in the MX record is allowed to send messages on behalf of Doe's family.

```shell
doe-family.com.          TXT "v=spf1 +mx -all"
```

> TODO: add commands

For incoming messages, SPF is configured to check that the sending host is authorized to use the `doe-family.com` according to published SPF policy. Rules are executed at the `mail` stage.

Edit the `/etc/vsmtp/domain-enabled/filter.vsl` file and add the following rule.

```
#{
  mail: [
    rule "check spf" || check_spf("both", "soft"),
  ]
}
```

<p class="ann"> Preventing spams using SPF </p>

> See the [`check_spf`][check_spf_fn_ref] reference for more details.

[check_spf_fn_ref]: ../../ref/vSL/api/fn::global.md
