# Domain Name System configuration

vSMTP can manage complex DNS situations. The default configuration can be updated for each virtual domain.

> vSMTP relies on Benjamin Fry's [Trust-DNS] crate to handle DNS queries.

DNS parameters are stored in the `[server.dns]` and `[server.virtual.dns]` tables and sub-tables. Please refer to vSMTP reference guide and [Trust-DNS] repository for detailed information.

[Trust-DNS]: (https://github.com/bluejekyll)

## DNS resolver

The default behavior is to use the operating system (/etc/resolv.conf) as the upstream resolvers. However other configuration are available and can be easily changed to:

- Google Public DNS
- The CloudFlare Public DNS
- A fully customized resolver

```toml
[server.dns]
type = "system" | "google" | "cloudflare"
```

Please see Google and CloudFlare privacy statement for important information about what they track.

### Resolver options

DNS Options can be set in the TOML `[server.dns.options]` and `[server.virtual.dns.options]` tables.

| Parameter | value | Description | Default value
| :--- | :--- | :--- | :--- |
| timeout | integer | Specify the timeout for a request. | 5 seconds.
| attempts | integer | usize Number of retries after lookup failure before giving up. | 2 attemps.
| rotate | true/false | Rotate through the resource records in the response. | No rotation.
| validate | true/false | Use DNSSec to validate the request. | False.
| ip_strategy | enum[^ip] | The ip_strategy for the Resolver to use when lookup Ipv4 or Ipv6 addresses. | IPv4 then IPv6.
| cache_size | integer | Cache size is in number of records. | 32 records.
| num_concurrent_reqs | integer | Number of concurrent requests per query. | 2 concurrent requests.
| preserve_intermediates | true/false | Preserve all intermediate records in the lookup response, suchas CNAME records. | True.

[^ip]: Ipv4Only, Ipv6Only, Ipv4AndIpv6, Ipv6thenIpv4, Ipv4thenIpv6

A Resolver configuration example :

```toml
[server.dns]
type = "cloudflare"

[server.dns.options]
timeout = "5s"
cache_size = 500
ip_strategy = "Ipv6thenIpv4"
validate = true
```

Advanced parameters are available. Please check vSMTP reference guide and [Trust-DNS] repository.

### DNS and SMTP return codes

In case of a DNS failure, the [RFC 3463], Enhanced Mail System Status Codes, registers two specific SMTP return codes.

[RFC 3463]: https://www.rfc-editor.org/rfc/rfc3463.html

| Code | X.4.3 |
| :--- | :--- |
| Text | Directory server failure |
| Basic status code | 451, 550 |
| Description | The network system was unable to forward the message, because a directory server was unavailable. This is useful only as a persistent transient error. The inability to connect to an Internet DNS server is one example of the directory server failure error.

| Code | X.4.4 |
| :--- | :--- |
| Text | Unable to route |
| Basic status code | not given |
| Description | The mail system was unable to determine the next hop for the message because the necessary routing information was unavailable from the directory server. This is useful for both permanent and persistent transient errors. A DNS lookup returning only an SOA (Start of Administration) record for a domain name is one example of the unable to route error.

> Available ? how ? TOML ?

## Locating the target host

[Section 5 of RFC5321] covers the sequence for identifying a server that accepts email for a domain. In essence, the SMTP client first looks up a DNS MX RR, and, if that is not found, it falls back to looking up a DNS A or AAAA RR.

[Section 5 of RFC5321]: https://www.rfc-editor.org/rfc/rfc5321#section-5

This mechanims has two major defects.

- It overloads a DNS record with an email service semantic.
- If there are no SMTP listeners at the A/AAAA addresses, message delivery will be attempted repeatedly many times before the sending Mail Transfer Agent (MTA) gives up and:
  - It delay notification to the sender in the case of misdirected mail.
  - It consumes resources at the sender.

vSMTP allows not to fall back to A and AAAA records with the `follow_A_AAAA` directive. However the "Null MX" protocol solves these issues.

### Null MX record

Basically the "null MX" protocol is a simple mechanism by which a domain can indicate that it does not accept email. It is described in [RFC 7505].

[RFC 7505]: https://www.rfc-editor.org/rfc/rfc7505.html

This protocol defines a null MX that will cause all mail delivery attempts to a domain to fail immediately.

A "Null NX" DNS record looks like :

```dns
nomail.example.com. 86400 IN MX 0 "."
```

vSMTP `enable_null_MX` directive allows to enable or disable this protocol.

#### Sender with "Null MX" records

As Null MX is primarily intended for domains that do not send or receive any mail, vSMTP default behavior is to reject mail that has an invalid return address. It can be changed with the `allow_null_MX_sender` directive.

However mail systems should not publish a null MX record for domains that they use in RFC5321.MailFrom or RFC5322.From addresses. If a system nonetheless does so, it risks having its mail rejected.

#### Null MX return codes

The RFC 7505 defines two specific return codes.

[Null MX]: https://www.rfc-editor.org/rfc/rfc7505.html

| Code | X.1.10 |
| :--- | :--- |
| Text | Recipient address has null MX |
| Basic status code | 556 |
| Description | The associated address is marked as invalid using a null MX.

| Code | X.7.27 |
| :--- | :--- |
| Text | Sender address has null MX |
| basic status code | 550
| Description | The associated sender address has a null MX, and the SMTP receiver is configured to reject mail from such sender (e.g., because it could not return a DSN).

> Null MX record feature and its status codes will be implemented in v0.11.

### CNAME record

As described in [Section 5 of RFC5321] if a CNAME record is found, the resulting name is processed as if it were the initial name. This behavior can be changed with the vSMTP directive `follow_CNAME`.

### Standard configuration

The example below shows how the default policy for locating the target host is implemented.

```toml
[server.dns.target]  ???????
follow_CNAME = false
follow_A_AAAA = false
enable_null_MX = true
allow_null_MX_sender = false
```

Note that is `enable_null_MX` policy is set to true, `follow_A_AAAA` is automatically set to false.

## Reverse DNS queries

Most email authentication mechanisms rely on reverse DNS queries. The configuration of these protocol-related queires is registered in their corresponding TOML tables.

However, for specific  DNS reverse queries can also be directly using the vSL reverse lookup function.

[RFC 7372] registers status codes to be returned if a message is being rejected or deferred specifically because of email authentication failures.

[RFC 7372]: https://www.rfc-editor.org/rfc/rfc7372.html

| Code | X.7.25 |
| :--- | :--- |
| Text | Reverse DNS validation failed |
| Basic status code | 550 |
| Description | An SMTP client's IP address failed a reverse DNS validation check, contrary to local policy requirements. |

> Available ? how ? TOML ?

Protocol-specific return codes are described in the corresponding chapters.

## vSL integration

> DNS queries and directives will be integrated to vSL in release 0.12.
