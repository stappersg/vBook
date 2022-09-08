# Complete vSMTP TOML key/value list

The behavior of your server can be configured using a configuration file,
and using the `-c, --config` flag of the `vsmtp`.

All the [parameters](#parameters) are optional and have default values.
If `-c, --config` is not provided, the default values of the configuration will be used.

The configuration file will be read and parsed right after starting the program,
producing an error if there is an invalid syntax, a filepath failed to be opened,
or any kind of errors.

If you have a non-explicit error when you start your server, you can create an issue
on the [github repo](https://github.com/viridIT/vSMTP), or ask for help in our discord server.

## Format

The configuration file format is [TOML](https://toml.io).

## Examples

You will find [examples here](https://github.com/viridIT/vSMTP/tree/develop/examples/config) and
the [technical documentation here](https://docs.rs/crate/vsmtp-config/latest).

## Parameters

### `version_requirement`

The **only mandatory** parameter to provide. This parameter is follow the [semver format](https://semver.org).
It is used to specify the version require of `vsmtp` to parse successfully this file.

Example:

```toml
version_requirement = ">=1.0.0, <2.0.0"
```

### `server.domain`

Example:

```toml
[server]
domain = "mydomain.com"
```

### `server.client_count_max`

```toml
[server]
client_count_max = 16
```

### `server.system`

```toml
[server.system]
user = "vsmtp"
group = "vsmtp"
group_local = "vsmtp"
```

### `server.system.thread_pool`

```toml
[server.system.thread_pool]
receiver = 6
processing = 6
delivery = 6
```

### `server.interfaces`

vSMTP can be used as a [MTA](../term/agent.md#mta-mail-transfer-agent) and/or a [MSA](../term/agent.md#msa-mail-submission-agent).

A MTA listen on port 25, and using server side authentication (SPF / DKIM / DMARC ...) to be protected from spam and identity substitution.

A MSA listen on port 587 and 465 (with TLS tunnel), in the same fashion than HTTP over port 80 and HTTPS over 443.
On these ports, stronger policies apply and client side authentication (SASL) is required.

Expose your public addresses here, (support both ipv4 and ipv6) :

```toml
[server.interfaces]
addr = ["192.168.1.254:25"]                  # <---- MTA's addresses
addr_submission = ["192.168.1.254:587"]      # <---- MSA's addresses
addr_submissions = ["192.168.1.254:465"]     # <---- MSA's addresses for SMTPS
```

These field are arrays, and you can leave any of them empty.
Make sure to provide at least **one address**, otherwise an error will be produced on startup.

You might want to add local address (`127.0.0.1:25` for example) when using delegation services.

### `server.logs`

```toml
[server.logs]
filepath = "/var/log/vsmtp/vsmtp.log"
level = [
    "info",
    "vsmtp_server::receiver=info",
    "vsmtp_rule_engine=warn",
    "vsmtp_delivery=error",
]
```

### `server.queues.dirpath`

```toml
[server.queues]
dirpath = "/var/spool/vsmtp"
```

### `server.queues.working`

```toml
[server.queues.working]
channel_size = 32
```

### `server.queues.delivery`

```toml
[server.queues.delivery]
channel_size = 32
deferred_retry_max = 100
deferred_retry_period = "5m"
```

### `server.tls`

```toml
[server.tls]
security_level = "Encrypt"
preempt_cipherlist = false
handshake_timeout = "200ms"
protocol_version = "TLSv1.3"
certificate = "/etc/vsmtp/tls/domain.com.certificate.crt"
private_key = "/etc/vsmtp/tls/domain.com.private_key.key"
```

### `server.virtual`

```toml
[server.virtual."mta1.domain.com"]

[server.virtual."mta2.domain.com".dns]
type = "system"

[server.virtual."mta3.domain.com".tls]
protocol_version = "TLSv1.3"
certificate = "/etc/vsmtp/tls/mta3.domain.com.certificate.crt"
private_key = "/etc/vsmtp/tls/mta3.domain.com.private_key.key"

[server.virtual."mta4.domain.com".tls]
protocol_version = "TLSv1.3"
certificate = "/etc/vsmtp/tls/mta4.domain.com.certificate.crt"
private_key = "/etc/vsmtp/tls/mta4.domain.com.private_key.key"

[server.virtual."mta4.domain.com".dns]
type = "google"
```

### `server.smtp`

```toml
[server.smtp]
rcpt_count_max = 1000
disable_ehlo = false
required_extension = ["STARTTLS", "SMTPUTF8", "8BITMIME", "AUTH"]
```

### `server.smtp.error`

```toml
[server.smtp.error]
soft_count = 10
hard_count = 20
delay = "5s"
```

### `server.smtp.timeout_client`

```toml
[server.smtp.timeout_client]
connect = "5m"
helo = "5m"
mail_from = "5m"
rcpt_to = "5m"
data = "5m"
```

### `server.smtp.auth`

```toml
[server.smtp.auth]
must_be_authenticated = true
enable_dangerous_mechanism_in_clair = true
mechanism = ["PLAIN", "LOGIN", "CRAM-MD5", "ANONYMOUS"]
```

### `server.dns`

```toml
[server.dns]
type = "custom"

[server.dns.config]
domain = "example.dns.com"
search = ["example.dns.com"]
name_servers = []

[server.dns.options]
# Sets the number of dots that must appear (unless it's a final dot representing the root)
#  that must appear before a query is assumed to include the TLD. The default is one, which
#  means that `www` would never be assumed to be a TLD, and would always be appended to either
#  the search
ndots = 1
# Number of retries after lookup failure before giving up. Defaults to 2
attempts = 2
# Rotate through the resource records in the response (if there is more than one for a given name)
rotate = false
# Enable edns, for larger records
edns0 = false
# Use DNSSec to validate the request
validate = false
# The ip_strategy for the Resolver to use when lookup Ipv4 or Ipv6 addresses
ip_strategy = "Ipv4thenIpv6"
# Cache size is in number of records (some records can be large)
cache_size = 32
# Check /ect/hosts file before dns requery (only works for unix like OS)
use_hosts_file = true
# Number of concurrent requests per query
#
# Where more than one nameserver is configured, this configures the resolver to send queries
# to a number of servers in parallel. Defaults to 2; 0 or 1 will execute requests serially.
num_concurrent_reqs = 2
# Preserve all intermediate records in the lookup response, suchas CNAME records
preserve_intermediates = true
# Try queries over TCP if they fail over UDP.
try_tcp_on_error = false
```

### `app.dirpath`

```toml
[app]
dirpath = "/var/spool/vsmtp/app"
```

### `app.vsl`

```toml
[app.vsl]
filepath = "/etc/vsmtp/main.vsl"
```

### `app.logs`

```toml
[app.logs]
filepath = "/var/log/vsmtp/app.log"
level = "WARN"
format = "{d} - {m}{n}"
size_limit = 10485760
archive_count = 10
```
