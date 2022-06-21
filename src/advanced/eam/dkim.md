# DomainKeys Identified Message

> ___This is a DRAFT for future releases. Support is planned for Q3/2022.___

This document specifies the vSMTP implementation of the DomainKeys Identified Mail Signatures (DKIM) protocol described in [RFC 6376](https://www.rfc-editor.org/rfc/rfc6376.html).

DKIM is an open standard for email authentication that verifies the message of an email. DKIM gives emails a signature header which is added to the email. This signature is secured by a key pair (private/public) and a certificate.

> DKIM signatures work like a watermark. Therefore, they survive forwarding, which is not the case for SPF.

Assertion of responsibility is validated through a cryptographic signature and by querying the Signer's domain directly to retrieve the appropriate public key.

## DNS records

Like the SPF protocol, DKIM is a DNS TXT record inserted into the sender domain's DNS. It contains the public key for the DKIM settings. The private key held by the sending email server can be verified against the public key by the receiving email server.

DKIM selectors are used to connect and decrypt encrypted signatures.

Unlike SPF authentication, your domain can have multiple DNS DKIM records without causing a problem.

A domain can have multiple public keys if it has multiple mail servers (each mail server has its own private key that matches only one public key). A selector is an attribute within a DKIM signature that helps the recipient's server find the correct public key in the sender's DNS.

A DKIM record must be placed in at address : `[selector]._domainkey.[domain].` and the query on may only result in one TXT type record maximum.

> DKIM keys are not meant to be changed frequently. A high time-to-live (TTL) value of 86400 seconds or more is not uncommon.

Here is an example of a DKIM record:

```shell
mail._domainkey.example.com. 86400 IN TXT "v=DKIM1; k=rsa; p=MIIBIjANBgkqhkiG...
```

For detailed information about fields in a DKIM record please check the [RFC 6376](https://www.rfc-editor.org/rfc/rfc6376.html#section-3.5).

## vSMTP implementation

vSMTP can act as `signer` or `verifier` as described in the RFC.

### Results of Evaluation

The vSMTP DKIM verifier implements results semantically equivalent to the RFC.

| Result    | Description                                                                                                                                                                                                  |
| :-------- | :----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| none      | The message was not signed.                                                                                                                                                                                  |
| pass      | The message was signed, the signature or signatures were acceptable to the ADMD, and the signature(s) passed verification tests.                                                                             |
| fail      | The message was signed and the signature or signatures were acceptable to the ADMD, but they failed the verification test(s).                                                                                |
| policy    | The message was signed, but some aspect of the signature or signatures was not acceptable to the ADMD.                                                                                                       |
| neutral   | The message was signed, but the signature or signatures contained syntax errors or were not otherwise able to be processed.  This result is also used for other failures not covered elsewhere in this list. |
| temperror | The message could not be verified due to some error that is likely transient in nature, such as a temporary inability to retrieve a public key.  A later attempt may produce a final result.                 |
| permerror | The message could not be verified due to some error that is unrecoverable, such as a required header field being absent. A later attempt is unlikely to produce a final result.                              |

### Results headers

Results should be recorded in the message header before any existing DKIM-Signature or preexisting
authentication status header fields in the header field block.

Unlike SPF there's no specific DKIM header thus the `Authentication-Results` header described in [RFC 8601](https://www.rfc-editor.org/rfc/rfc8601#appendix-B) should be used.

```shell
Authentication-Results: example.com;
            dkim=pass (good signature) header.d=example.com
Received: from mail-router.example.com
                (mail-router.example.com [192.0.2.1])
            by auth-checker.example.com (8.11.6/8.11.6)
                with ESMTP id i7PK0sH7021929;
            Fri, Feb 15 2002 17:19:22 -0800
DKIM-Signature:  v=1; a=rsa-sha256; s=gatsby; d=example.com;
            t=1188964191; c=simple/simple; h=From:Date:To:Subject:
            Message-Id:Authentication-Results;
            bh=sEuZGD/pSr7ANysbY3jtdaQ3Xv9xPQtS0m70;
            b=EToRSuvUfQVP3Bkz ... rTB0t0gYnBVCM=
```

### DKIM failure codes

The [RFC 7372](https://www.rfc-editor.org/rfc/rfc7372.html#section-3) "Email Auth Status Codes" introduces new status codes for reporting the DKIM and SPF mechanisms.

| Code              | X.7.20                                                 |
| :---------------- | :----------------------------------------------------- |
| Text              | No passing DKIM signature found                        |
| Basic status code | 550                                                    |
| Description       | A message did not contain any passing DKIM signatures. |

| Code              | X.7.21                                                                           |
| :---------------- | :------------------------------------------------------------------------------- |
| Text              | No acceptable DKIM signature found                                               |
| Basic status code | 550                                                                              |
| Description       | A message contains one or more passing DKIM signatures, but none are acceptable. |

| Code              | X.7.22                                                                                                                                                                                 |
| :---------------- | :------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Text              | No valid author-matched DKIM signature found.                                                                                                                                          |
| Basic status code | 550                                                                                                                                                                                    |
| Description       | A message contains one or more passing DKIM signatures, but none are acceptable because none have an identifier(s) that matches the author address(es) found in the From header field. |

The following error codes can also be sent by the DKIM framework.

| Code              | X.7.25                                                                                                    |
| :---------------- | :-------------------------------------------------------------------------------------------------------- |
| Text              | Reverse DNS validation failed                                                                             |
| Basic status code | 550                                                                                                       |
| Description       | An SMTP client's IP address failed a reverse DNS validation check, contrary to local policy requirements. |
| Used in place of  | n/a                                                                                                       |

| Code              | X.7.26                                                                                                                                                       |
| :---------------- | :----------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Text              | Multiple authentication checks failed                                                                                                                        |
| Basic status code | 500                                                                                                                                                          |
| Description       | A message failed more than one message authentication check, contrary to local policy requirements. The particular mechanisms that failed are not specified. |
| Used in place of  | n/a                                                                                                                                                          |
