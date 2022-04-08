# Domain Name System configuration

vSMTP can manage complex DNS situations. The default configuration can be updated for each virtual domain. DNS parameters are stored in the `[server.dns.config]` and `[server.virtual.dns.config]`tables.

> vSMTP relies on Benjamin Fry's [Trust-DNS] crate to handle DNS queries. 

Please refer to vSMTP reference guide and [Trust-DNS] repository for detailed information.

[Trust-DNS]: (https://github.com/bluejekyll)

## DNS resolver

The default behavior is to use the operating system (/Etc/resolv.conf) as the upstream resolvers. However using the `type` keyword this can be easily changed to:

- Google Public DNS
- The CloudFlare Public DNS
- A fully customized resolver

```toml
[server.dns]
type = "system" | "custom" | "google" | "cloudflare"
```

Please see Google and CloudFlare privacy statement for important information about what they track.

## Available options

DNS Options can be set in the TOML `[server.dns.options]` and `[server.virtual.dns.options]` tables.


| Parameter | value | Description |
| :--- | :--- | :--- |
| timeout | integer | Specify the timeout for a request. Defaults to 5 seconds.
| attempts | integer | usize Number of retries after lookup failure before giving up. Defaults to 2.
| rotate | true/false | Rotate through the resource records in the response. Defaults to `XXXXX`
| validate | true/false | Use DNSSec to validate the request. Defaults to `XXXXX`
| ip_strategy | enum[^ip] | The ip_strategy for the Resolver to use when lookup Ipv4 or Ipv6 addresses
| cache_size | integer | Cache size is in number of records.
| num_concurrent_reqs | integer | Number of concurrent requests per query. Defaults to 2.
| preserve_intermediates | true/false | Preserve all intermediate records in the lookup response, suchas CNAME records. Defaults to `XXXXX`

[^ip]: Ipv4Only, Ipv6Only, Ipv4AndIpv6, Ipv6thenIpv4, Ipv4thenIpv6

Example :

```toml
[server.dns]
type = cloudflare

[server.dns.options]
timeout = 5s
cache_size = 500
ip_strategy = "Ipv6thenIpv4"
```

Advanced parameters are available. Please check vSMTP reference guide and [Trust-DNS] repository for detailed 
information.

[Trust-DNS]: (https://github.com/bluejekyll)

