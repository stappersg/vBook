# Using the Sender Policy Framework

`SPF` allows other MTAs to check that outgoing messages from Doe's family domain are valid.

A new DNS record is added into the `doe-family.com` DNS zone. It declares that only the server specified in the MX record is allowed to send messages on behalf of Doe's family.

```shell
doe-family.com.          TXT "v=spf1 +mx -all"
```

For incoming messages, SPF is configured to check that the sending host is authorized to use the `doe-family.com` according to published SPF policy. Rules are executed at the `mail` stage.

Edit the `/etc/vsmtp/domain-available/incoming.vsl` file and add the following rule.
```js
#{
  mail: [
    rule "check spf" || check_spf("both", "soft"),
  ]
}
```
<p style="text-align: center;"> <i>Preventing spams using SPF</i> </p>

> Check out the [Security module](/src/reference/vSL/api/Security.md) for more details on the `check_spf` function.

## Further details

This document describes the vSMTP implementation of the Sender Policy Framework (SPF) protocol described in [RFC 7208](https://www.rfc-editor.org/rfc/rfc7208.html).

SPF is an authentication standard used to link a domain name and an email address. it allows email clients to verify that incoming email from a domain comes from a host authorized by the administrator of this domain.

The SPF framework allows the ADministrative Management Domains (ADMDs) to explicitly authorize hosts to send email. The authorization list is published in the DNS records of the sender's domain.

### DNS records

The type of a SPF record is TXT. There should be only one SPF record per domain. In case of multiple SPF records, an error may be raised.

Here is a basic SPF record example: "only servers in the range 123.123.123.0/24 and MTA (MX) are authorized to send emails from my domain example.com. All other senders are considered unauthorized."

```shell
example.com.          TXT "v=spf1 +mx ip4:123.123.123.0/24 -all"
```

There is also a tilde version: ~all. It warns that other senders are not allowed, but must still be accepted. This “Soft Fail” statement was first introduced for testing purposes, but is now used by various hosting providers.

> Use of wildcard records for publishing is discouraged.

Please refer to RFC 7208 for further details.

### vSMTP implementation

#### HELO/EHLO Identity

The RFC 7208 does not enforce a HELO/EHLO verification.

> "It is RECOMMENDED that SPF verifiers not only check the "MAIL FROM" identity but also separately check the "HELO" identity
[...] Additionally, since SPF records published for "HELO" identities refer to a single host, when available, they are a very reliable source of host authorization status.  Checking "HELO" before "MAIL FROM" is the RECOMMENDED sequence if both are checked."

The RFC 5321 tends to normalize the HELO/EHLO arguments to represent the fully qualified domain name of the SMTP client. However the vSMTP SPF verifier is prepared for the identity to be an IP address literal or simply be malformed.

> "SPF check can only be performed when the "HELO" string is a valid, multi-label domain name."

#### MAIL FROM identity

According to the RFC, "MAIL FROM" check occurs when :

> "SPF verifiers MUST check the "MAIL FROM" identity if a "HELO" check either has not been performed or has not reached a definitive policy result."

Note that [RFC5321](https://www.rfc-editor.org/rfc/rfc5321.html#section-4.5.5) allows the reverse-path to be null. In this case, the RFC 7208 defines the "MAIL FROM" identity as the local-part "postmaster" and the "HELO" identity.

#### Location of checks

As defined by the RFC :

> "The authorization check SHOULD be performed during the processing of the SMTP transaction that receives the mail. This reduces the complexity of determining the correct IP address to use as an input to check_host() and allows errors to be returned directly to the sending MTA by way of SMTP replies."

vSMTP allows the use of the SPF framework only at the "MAIL FROM" stage.

#### Results of Evaluation

The vSMTP SPF verifier implements results semantically equivalent to the RFC.

| Result    | Description                                                                                                                                                                                                                                                                                                                                                    |
| :-------- | :------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| none      | (a) no syntactically valid DNS domain name was extracted from the SMTP session that could be used as the one to be or (b) no SPF records were retrieved from the DNS.                                                                                                                                                                                          |
| neutral   | The ADMD has explicitly stated that it is not asserting whether the IP address is authorized.                                                                                                                                                                                                                                                                  |
| pass      | The client is authorized to inject mail with the given identity.                                                                                                                                                                                                                                                                                               |
| fail      | The client is not authorized to use the domain in the given identity.                                                                                                                                                                                                                                                                                          |
| softfail  | The host is probably not authorized but the ADMD has not published a stronger policy.                                                                                                                                                                                                                                                                          |
| temperror | A transient (generally DNS) error while performing the check.                                                                                                                                                                                                                                                                                                  |
| permerror | The domain's published records (DNS) could not be correctly interpreted.                                                                                                                                                                                                                                                                                       |
| policy    | Added by [RFC 8601, Section 2.4](https://www.rfc-editor.org/rfc/rfc8601#section-2.4) - indicate that some local policy mechanism was applied that augments or even replaces (i.e., overrides) the result returned by the authentication mechanism.  The property and value in this case identify the local policy that was applied and the result it returned. |

#### Results headers

Results should be recorded in the message header. Two options are available according to the RFC:

1. The "Received-SPF" header

```shell
Received-SPF: pass (mybox.example.org: domain of myname@example.com
  designates 192.0.2.1 as permitted sender)
  receiver=mybox.example.org; client-ip=192.0.2.1;
  envelope-from="myname@example.com"; helo=foo.example.com;
```

1. The "Authentication-Results" header described in [RFC 8601](https://www.rfc-editor.org/rfc/rfc8601#appendix-B) : Message Header Field for Indicating Message Authentication Status.

```shell
Authentication-Results: example.com; spf=pass smtp.mailfrom=example.net
```

#### SPF failure codes

The [RFC 7372](https://www.rfc-editor.org/rfc/rfc7372.html#section-3) "Email Auth Status Codes" introduces new status codes for reporting the DKIM and SPF mechanisms.

| Code              | X.7.23                                                                                                                                 |
| :---------------- | :----------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Text              | SPF validation failed                                                                                                                  |
| Basic status code | 550                                                                                                                                    |
| Description       | A message completed an SPF check that produced a "fail" result                                                                         |
| Used in place of  | 5.7.1, as described in Section 8.4 of RFC 7208.                                                                                        |

| Code              | X.7.24                                                                                                                                 |
| :---------------- | :----------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Text              | SPF validation error                                                                                                                   |
| Basic status code | 451/550                                                                                                                                |
| Description       | Evaluation of SPF relative to an arriving message resulted in an error.                                                                |
| Used in place of  | 4.4.3 or 5.5.2, as described in Sections 8.6 and 8.7 of RFC 7208.                                                                      |

The following error codes can also be sent by the SPF framework.

| Code              | X.7.25                                                                                                                                 |
| :---------------- | :----------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Text              | Reverse DNS validation failed                                                                                                          |
| Basic status code | 550                                                                                                                                    |
| Description       | An SMTP client's IP address failed a reverse DNS validation check, contrary to local policy requirements.                              |
| Used in place of  | n/a                                                                                                                                    |

| Code              | X.7.26                                                                                                                                                       |
| :---------------- | :----------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Text              | Multiple authentication checks failed                                                                                                                        |
| Basic status code | 500                                                                                                                                                          |
| Description       | A message failed more than one message authentication check, contrary to local policy requirements. The particular mechanisms that failed are not specified. |
| Used in place of  | n/a                                                                                                                                                          |
