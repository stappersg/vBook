# DomainKeys Identified Message

> ___This is DRAFT for v0.11 features___

This document specifies the vSMTP implementation of the DomainKeys Identified Mail Signatures (DKIM) protocol described in [RFC 6376](https://www.rfc-editor.org/rfc/rfc6376.html).

The DomainKeys Identified Mail (DKIM) is an open standard for email authentication that verifies the message of an email. DKIM gives emails a signature header which is added to the email. This signature is secured by a key pair (private/public) and a certificate. 

> DKIM signatures work like a watermark. Therefore, they survive forwarding, which is not the case for SPF, another standard for email authentication.

Assertion of responsibility is validated through a cryptographic signature and by querying the Signer's domain directly to retrieve the appropriate public key.


## DNS records

Like the SPF protocol, DKIM is a DNS TXT record inserted into the sender domain's DNS. It contains the public key for the DKIM settings. The private key held by the sending email server can be verified against the public key by the receiving email server.

DKIM selectors are used to connect and decrypt encrypted signatures.

Here is a basic SPF record example. Please refer to RFC 7208 for further details.

```shell
example.com.          TXT "v=spf1 +mx ip4:123.123.123.0/24 -all"
```

It means "only servers in the range 123.123.123.0/24 and MTA (MX) are authorized to send emails from my domain example.com. All senders not listed here are considered unauthorized. "

Besides the aforementioned "-all" there is also a tilde version: ~all. It indicates that other senders are not allowed, but must still be accepted. This “Soft Fail” statement was first introduced for testing purposes, but is now used by various hosting providers.

> Use of wildcard records for publishing is discouraged.

## vSMTP implementation

### HELO/EHLO Identity

The RFC 7208 does not enforce a HELO/EHLO verification.

> "It is RECOMMENDED that SPF verifiers not only check the "MAIL FROM" identity but also separately check the "HELO" identity
[...] Additionally, since SPF records published for "HELO" identities refer to a single host, when available, they are a very reliable source of host authorization status.  Checking "HELO" before "MAIL FROM" is the RECOMMENDED sequence if both are checked."

Even if the RFC 5321 tends to normalize the HELO/EHLO arguments as the fully qualified domain name of the SMTP client, the vSMTP SPF verifier is prepared for the identity to be an IP address literal or simply be malformed.  

> "SPF check can only be performed when the "HELO" string is a valid, multi-label domain name."

Despite what RFC 7208 explains, the vSMTP SPF checker can also work with IP addresses.

### MAIL FROM identity

According to RFC, "MAIL FROM" check occurs when :

> "SPF verifiers MUST check the "MAIL FROM" identity if a "HELO" check either has not been performed or has not reached a definitive policy result."

Please notes that [RFC5321](https://www.rfc-editor.org/rfc/rfc5321.html#section-4.5.5) allows the reverse-path to be null. In this case, the RFC 7208 defines the "MAIL FROM" identity to be the mailbox composed of the local-part "postmaster" and the "HELO" identity.

### Location of checks

As defined by the RFC :

> "The authorization check SHOULD be performed during the processing of the SMTP transaction that receives the mail. This reduces the complexity of determining the correct IP address to use as an input to check_host() and allows errors to be returned directly to the sending MTA by way of SMTP replies."

vSMTP allows utilization of the SPF framework only at the "MAIL FROM" stage.

### Results of Evaluation

The vSMTP SPF verifier implements results semantically equivalent to the RFC.

| Result | Statement | Description |
| :--- | :--- | :--- |
| None | Explicit | (a) no syntactically valid DNS domain name was extracted from the SMTP session that could be used as the one to be or (b) no SPF records were retrieved from the DNS.|
| Neutral | Explicit | The ADMD has explicitly stated that it is not asserting whether the IP address is authorized. |
| Pass | Explicit | The client is authorized to inject mail with the given identity. |
| Fail | Explicit | The client is not authorized to use the domain in the given identity. |
| Softfail | Weak | The host is probably not authorized but the ADMD has not published a stronger policy. |
| Temperror | Weak | A transient (generally DNS) error while performing the check. |
| Permerror | Explicit | The domain's published records (DNS) could not be correctly interpreted. |

### Results headers

Results should be recorded in the message header. According to RFCs, two options are available :

1. The "Received-SPF" header

```shell
Received-SPF: pass (mybox.example.org: domain of myname@example.com designates 192.0.2.1 as permitted sender)
receiver=mybox.example.org; client-ip=192.0.2.1; envelope-from="myname@example.com"; helo=foo.example.com;
```

2. The "Authentication-Results" header described in [RFC 8601](https://www.rfc-editor.org/rfc/rfc8601#appendix-B) : Message Header Field for Indicating Message Authentication Status.

```shell
Authentication-Results: example.com; spf=pass smtp.mailfrom=example.net
```

### SPF failure codes

The [RFC 7372]() "Email Auth Status Codes" introduces new status codes for reporting the DKIM and SPF mechanisms.

| Code | X.7.23 |
| :--- | :--- |
| Sample Text | SPF validation failed |
| Associated basic status code | 550 |
| Description | A message completed an SPF check that produced a "fail" result |
| Used in place of| 5.7.1, as described in Section 8.4 of RFC 7208.|

| Code | X.7.24 |
| :--- | :--- |
| Sample Text | SPF validation error |
| Associated basic status code | 451/550 |
| Description | Evaluation of SPF relative to an arriving message resulted in an error. |
| Used in place of | 4.4.3 or 5.5.2, as described in Sections 8.6 and 8.7 of RFC 7208. |

The following error codes can also be sent by the SPF framework.

| Code | X.7.25 |
| :--- | :--- |
| Sample Text | Reverse DNS validation failed |
| Associated basic status code | 550 |
| Description | An SMTP client's IP address failed a reverse DNS validation check, contrary to local policy requirements. |
| Used in place of | n/a |

| Code | X.7.26 |
| :--- | :--- |
| Sample Text | Multiple authentication checks failed |
| Associated basic status code | 500
| Description | A message failed more than one message authentication check, contrary to local policy requirements. The particular mechanisms that failed are not specified. |
| Used in place of | n/a |

## vSMTP example

```toml
[app.spf]
spf_enable = "yes | no"
check_helo = "yes | no"
allow_helo_ip = "yes | no"
check_mailfrom = "yes | no"
spf_policy = "helo | mail | mail OR helo | mail AND helo"
header_result = "no | received-spf | authentication-results | both"
```

```rust
rule mail "psf" blahblah {
    mslk  mlkm lk mlk mlk 
    mlsdmflk mlk mlsdk mlsdk
}
```
