# Domain Name System configuration

vSMTP can handle complex DNS situations. A default configuration can be provided on the root configuration of vSMTP and specific dns configurations can be setup on specific domains.

Root DNS parameters are stored in the `config.server.dns` map.

> Please refer to [vSMTP configuration reference] and [Trust-DNS] repository for detailed information.

[vSMTP configuration reference]: ../ref/vSL/api/var::cfg.md
[Trust-DNS]: https://github.com/bluejekyll/trust-dns

## Resolver

The default behavior of the root resolver is defined by the operating system `/etc/resolv.conf` file. Alternative configurations such as `Google` or `CloudFlare` Public DNS may be applied using the `type` field in the `server.dns` table.

```rust
fn on_config(config) {
  config.server.dns.type = "system" | "google" | "cloudflare";

  config
}
```
<p class="ann"> Selecting a DNS type </p>

> Please see `Google` and `CloudFlare` privacy statement for important information about what they track.

### Options

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
<p class="ann"> DNS parameters </p>

[^ip]: Ipv4Only, Ipv6Only, Ipv4AndIpv6, Ipv6thenIpv4, Ipv4thenIpv6

```rust,ignore
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
<p class="ann"> A Resolver configuration example </p>

## Domain specific resolver

It is possible to configure a DNS per domain. Under the desired domain folder in your `config.vsl`, add a `on_domain_config` callback and configure the dns here.

```rust,ignore
fn on_domain_config(config) {
  config.dns.type = "cloudflare";
  config.dns.options = #{
    timeout: "5s",
    cache_size: 500,
    ip_strategy: "Ipv6thenIpv4",
    validate: true,
  };

  config
}
```
<p class="ann"> A configuration for a specific domain, i.e. `/etc/vsmtp/domain-enabled/example.com/config.vsl` </p>
