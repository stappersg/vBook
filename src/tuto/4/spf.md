# Using the Sender Policy Framework

SPF is an authentication standard used to link a domain name and an email address. it allows email clients to verify that incoming email from a domain comes from a host authorized by the administrator of this domain.

In this tutorial, we will set up SPF for the `example.com` domain by:

- Adding DNS TXT records for SPF.
- Add filtering for incoming and outgoing emails using SPF.

Feel free to replace `example.com` by your own domain.

## Add a DNS TXT record for SPF

A new DNS record is added into the `example.com` DNS zone. It declares that only the server specified in the MX record is allowed to send messages on behalf of the domain.

```shell
example.com.          TXT "v=spf1 +mx -all"
```
<p class="ann"> A TXT record with SPF specifications for the `example.com` domain </p>

> TODO: add commands

## Filtering with SPF

For incoming messages, SPF is configured to check that the sending host is authorized to use the `example.com` domain according to published SPF policy. Rules are executed at the `mail` stage.

Edit the `/etc/vsmtp/filter.vsl` script and add the following rule.

```
#{
  mail: [
    rule "check spf" || spf::check("both", "soft"),
  ]
}
```
<p class="ann"> Preventing spams using SPF </p>

> See the [`spf::check`][check_spf_fn_ref] reference for more details.
>
> To check if DKIM is working correctly, check out [this site](https://appmaildev.com/en/spf).

[check_spf_fn_ref]: ./../../ref/vSL/api/fn::global::spf.md
