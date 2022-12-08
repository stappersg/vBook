# Domain Name System configuration

vSMTP can handle complex DNS situations. A default configuration is applied on the root domain and virtual domains inherit from it. Specific values can be updated on root domain or on a per virtual domain basis.

DNS parameters are stored in the `[server.dns]` and `[server.virtual.dns]` tables and sub-tables. Please refer to [vSMTP configuration reference] and [Trust-DNS] repository for detailed information.

[vSMTP configuration reference]: /src/ref/vSL/api/var::cfg.md

[Trust-DNS]: https://github.com/bluejekyll/trust-dns

## DNS resolver

The default behavior of the upstream resolver is defined by the operating system `/etc/resolv.conf` file. Alternative configurations such as Google or CloudFlare Public DNS may be applied using the `type` field in the `server.dns` table.

```rust
fn on_config(config) {
  config.server.dns.type = "system" | "google" | "cloudflare";

  config
}
```

Please see Google and CloudFlare privacy statement for important information about what they track.

### Locating the target host

[Section 5 of RFC5321] covers the sequence to identify a server that accepts email for a domain. The SMTP client first looks up a DNS MX RR, and if is not found, falls back to a DNS A or AAAA request. If a CNAME record is found, the resulting name is processed as if it were the initial name.

[Section 5 of RFC5321]: https://www.rfc-editor.org/rfc/rfc5321#section-5

This mechanism suffers from two major drawbacks.

- A DNS overload because of an email service semantic.
- If there are no SMTP listeners at the A/AAAA addresses, message delivery will be attempted repeatedly many times before the sending Mail Transfer Agent (MTA) gives up, implying:
  - a delay notification to the sender in the case of misdirected mail,
  - a waste of IT resources at the sender.

The "Null MX" protocol solves these issues.

### Resolver options

DNS Options can be set using the `config.server.dns.options` object.

| Parameter              | value      | Description                                                                      | Default value          |
| :--------------------- | :--------- | :------------------------------------------------------------------------------- | :--------------------- |
| timeout                | integer    | Specify the timeout for a request.                                               | 5 seconds.             |
| attempts               | integer    | usize Number of retries after lookup failure before giving up.                   | 2 attempts.            |
| rotate                 | true/false | Rotate through the resource records in the response.                             | No rotation.           |
| validate               | true/false | Use DNSSec to validate the request.                                              | False.                 |
| ip_strategy            | enum[^ip]  | The ip_strategy for the Resolver to use when lookup Ipv4 or Ipv6 addresses.      | IPv4 then IPv6.        |
| cache_size             | integer    | Cache size is in number of records.                                              | 32 records.            |
| num_concurrent_reqs    | integer    | Number of concurrent requests per query.                                         | 2 concurrent requests. |
| preserve_intermediates | true/false | Preserve all intermediate records in the lookup response, such as CNAME records. | True.                  |

[^ip]: Ipv4Only, Ipv6Only, Ipv4AndIpv6, Ipv6thenIpv4, Ipv4thenIpv6

A Resolver configuration example :

```rust
fn on_config(config) {
  config.server.dns.type = "cloudflare";
  config.server.dns.options = #{
    timeout: "5s",
    cache_size: 500,
    ip_strategy: "Ipv6thenIpv4",
    validate: true,
  };

  config
}
```

Advanced parameters are available. Please check vSMTP reference guide and [Trust-DNS] repository.

## DNS and SMTP return codes

In case of a DNS failure, the [RFC 3463], Enhanced Mail System Status Codes, registers two specific SMTP return codes.

[RFC 3463]: https://www.rfc-editor.org/rfc/rfc3463.html

| Code              | X.4.3                                                                                                                                                                                                                                                           |
| :---------------- | :-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Text              | Directory server failure.                                                                                                                                                                                                                                       |
| Basic status code | 451, 550                                                                                                                                                                                                                                                        |
| Description       | The network system was unable to forward the message, because a directory server was unavailable. This is useful only as a persistent transient error. The inability to connect to an Internet DNS server is one example of the directory server failure error. |

| Code              | X.4.4                                                                                                                                                                                                                                                                                                                                                           |
| :---------------- | :-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Text              | Unable to route.                                                                                                                                                                                                                                                                                                                                                |
| Basic status code | Not given.                                                                                                                                                                                                                                                                                                                                                      |
| Description       | The mail system was unable to determine the next hop for the message because the necessary routing information was unavailable from the directory server. This is useful for both permanent and persistent transient errors. A DNS lookup returning only an SOA (Start of Administration) record for a domain name is one example of the unable to route error. |

## Reverse DNS queries

Most email authentication mechanisms rely on reverse DNS queries. The configuration of these protocol-related queries is registered in their corresponding configuration objects.

However, for specific  DNS reverse queries can also be directly using the vSL reverse lookup function.

[RFC 7372] registers status codes to be returned if a message is being rejected or deferred specifically because of email authentication failures.

[RFC 7372]: https://www.rfc-editor.org/rfc/rfc7372.html

| Code              | X.7.25                                                                                                    |
| :---------------- | :-------------------------------------------------------------------------------------------------------- |
| Text              | Reverse DNS validation failed.                                                                            |
| Basic status code | 550                                                                                                       |
| Description       | An SMTP client's IP address failed a reverse DNS validation check, contrary to local policy requirements. |

Protocol-specific return codes are described in the corresponding chapters.
