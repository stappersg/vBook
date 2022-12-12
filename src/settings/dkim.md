# DomainKeys Identified Mail (DKIM)

DKIM is an open standard for email authentication used to check the integrity of the content of an email.
vSMTP exposes filtering rules and configuration to setup DKIM and secure your server.

## Key configuration

The path to a private key for DKIM can be specified in the `/etc/vsmtp/conf.d/config.vsl` script:

```rust,ignore
fn on_config(config) {
  config.server.dkim.private_key = ["/path/to/private-key-1", "/path/to/private-key-2", ...];
  config
}
```
<p class="ann"> Configuring DKIM keys </p>

You can also configure keys per domain.

```rust,ignore
fn on_domain_config(config) {
  config.dkim.private_key = ["/path/to/private-key-1", "/path/to/private-key-2", ...];
  config
}
```
<p class="ann"> Configuring DKIM keys for a specific domain (f.e. example.com)</p>

> If a key cannot be found for a specific domain, the root dkim keys are used instead.

> Check out the [`Using DKIM`](../tuto/3/dkim.md) tutorial to setup filtering using DKIM.