# SSL/TLS

Connections should be encrypted using the SSL/TLS protocol, even on a private network.

The vSMTP implementation is based on the state-of-the-art [rustls](https://docs.rs/rustls/latest/rustls) library.

Add the following to the `/etc/vsmtp/vsmtp.toml` file:

```toml
# ...

# TLS settings
[server.tls]
security_level = "May"
preempt_cipherlist = false
handshake_timeout = "1000ms"
protocol_version = ["TLSv1.2", "TLSv1.3"]
certificate = "/etc/letsencrypt/live/mta.doe-family.com/cert.pem"
private_key = "/etc/letsencrypt/live/mta.doe-family.com/privkey.pem"
```