# SMTP Security via Opportunistic DNS-Based Authentication of Named Entities (DANE) Transport Layer Security (TLS)

> ___This is a DRAFT for v0.12 features___

DNS-based Authentication of Named Entities (DANE) is designed to prevent snooping of email traffic by requiring the use of TLS encryption whenever possible during transport.

A client using DANE requests the public key of a server through the Domain Name System SECurity Extensions (DNSSEC) protocol. 

DANE introduces the DNS "TLSA" resource record (RR) type. This record associate a certificate or a public key of an end-entity or a trusted issuing authority with the corresponding Transport Layer Security (TLS) endpoint.

Trusted public certificate are not needed anymore.

## vSMTP implementation

### DANE TLSA Record Overview

TLSA resource records are stored at a prefixed DNS domain name. The records consist of four fields. The record type is determined by the values of the first three fields:

- The Certificate Usage field: PKIX-TA(0), PKIX-EE(1), DANE-TA(2), and DANE-EE(3).
- The Selector field:  Cert(0) and SPKI(1).  
- The Matching Type field : Full(0), SHA2-256(1), and SHA2-512(2).  

The latest field (Certificate Association Data) stores the full value or digest of the       certificate or subject public key as determined by the matching type and selector, respectively.

```shell
                                      |------- Certificate usage
              |-- Base domain name    | |----- Selector  
              |                       | | |--- Matching type  
              v                       v v v
   _25._tcp.mail.example.com. IN TLSA 2 0 1 (
    ^     ^                            E8B54E0B4BAA815B06D3462D65FBC7C0
    |     |-- Protocol                 CF556ECCF9F5303EBFBB77D022F834C0 )
    |                                      ^
    |-- Port                               |----- Certificate Association Data
```

vSMTP supports only DANE-TA(2) and DANE-EE(3) certificate usage.

This is implement by vSMTP using `key = value`and `key = value` in the TOML configuration file.

### DANE TLS Requirements

> TLS clients using DANE MUST support the SNI extension of TLS. Servers MAY support SNI and respond with a matching certificate chain but MAY also ignore SNI and respond with a default
certificate chain.  When a server supports SNI but is not configured with a certificate chain that exactly matches the client's SNI extension, the server SHOULD respond with another certificate chain (a default or closest match). This is because clients might support more than one server name but can only put a single name in the SNI extension.

These behaviors are set with the `key = value`and `key = value` in the TOML configuration file.

### Digest Algorithm Agility

As described in the RFC : 
> "Client implementations SHOULD implement a default order of digest algorithms by strength This order SHOULD be configurable by the administrator or user of the client software. If possible, a configurable mapping from numeric DANE TLSA matching types to underlying digest algorithms provided by the cryptographic library SHOULD be implemented to allow new matching types to be used with software that predates their introduction. Configurable ordering of digest algorithms SHOULD be extensible to any new digest algorithms."

This is implement by vSMTP using `key = value`and `key = value` in the TOML configuration file.

> Algorithm agility is to be applied after first discarding any unusable or malformed records (unsupported digest algorithm, or incorrect digest length).  For each usage and selector, the client SHOULD process only any usable records with a matching type of Full(0) and the usable records whose digest algorithm is considered by the client to be the strongest among usable records with the given usage and selector.

This is implement by vSMTP using `key = value`and `key = value` in the TOML configuration file.


## vSMTP example

```toml
/// toml
TO DO
```

```c
/// main.vsl
TO DO
```