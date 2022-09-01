# SSL/TLS

Except under closed network, you want your connection to be encrypted using SSL/TLS.

The vSMTP implementation is based on the state-of-the-art [rustls](https://docs.rs/rustls/latest/rustls) library.

Add the following to your `/etc/vsmtp/vsmtp.toml` file:

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
