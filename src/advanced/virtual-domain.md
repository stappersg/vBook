# Virtual Domain

As shown in the example below, virtual domains can be configured under the root domain.

```js
let config = new_config();

// Root domain.
config.server.domain = "root-example.net";

config.server.dns.type = "google";

config.server.tls.security_level = "None";

// ...
// ... End of main domain configuration

//
// Virtual domain : "example1.com"
//

// DNS type is not specified - thus it's inherited from the main domain.
config.server.virtual["example1.com"] = #{
    tls: #{
        protocol_version: "TLSv1.3",
        certificate: "./certs/certificate-example1.crt",
        private_key: "./certs/private-example2.key",
    }
};

//
// Virtual domain : "example2.com"
//
config.server.virtual["example2.com"] = #{
    dns: #{ type: "system" },
    tls: #{
        protocol_version: "TLSv1.3",
        certificate: "./certs/certificate-example2.crt",
        private_key: "./certs/private-example2.key",
    }
};
```

Parameters can be:

- Specified in primary domain: All virtual domains use these settings.
- Specific to a virtual domain.

Please refer to the [reference guide](../reference/config-file.md) for a fully description of the key/value pairs.
