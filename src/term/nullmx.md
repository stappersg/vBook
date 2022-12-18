# Null MX record

[Section 5 of RFC5321] covers the sequence to identify a server that accepts email for a domain. The SMTP client first looks up a DNS MX RR, and if is not found, falls back to a DNS A or AAAA request. If a CNAME record is found, the resulting name is processed as if it were the initial name.

This mechanism suffers from two major drawbacks.

- A DNS overload because of an email service semantic.
- If there are no SMTP listeners at the A/AAAA addresses, message delivery will be attempted repeatedly many times before the sending Mail Transfer Agent (MTA) gives up, implying:
  - a delay notification to the sender in the case of misdirected mail,
  - a waste of IT resources at the sender.

The "Null MX" protocol solves these issues. It is used to state that mail services are disabled in a given domain. The protocol is described in [RFC 7505].

[RFC 7505]: https://www.rfc-editor.org/rfc/rfc7505.html
[Section 5 of RFC5321]: https://www.rfc-editor.org/rfc/rfc5321#section-5

When a specific DNS record (a null MX) is effectively defined in the DNS zone of a given domain, all mail delivery attempts fail immediately.

## DNS record

The `null MX` RR is an ordinary MX record with an RDATA section consisting of preference number 0 and a "." as the exchange domain, to denote that there exists no mail exchanger.  

```dns
nomail.example.com. 86400 IN MX 0 "."
```

A domain that advertises a null MX __must not__ advertise any other MX RR.

## Sender with Null MX records

As Null MX is primarily intended for domains that do not send or receive any mail, vSMTP default behavior rejects mail that has an invalid return address.

Mail systems should not publish a null MX record for domains that they use in `MAIL FROM` (RFC5321) or `From` (RFC5322) directives.

## Return codes

The RFC 7505 defines two specific return codes.

[Null MX]: https://www.rfc-editor.org/rfc/rfc7505.html

| Code | X.1.10 |
| - | - |
| Text | Recipient address has null MX |
| Basic status code | 556 |
| Description | The associated address is marked as invalid using a null MX. |


| Code | X.7.27 |
| - | - |
| Text | Sender address has null MX |
| Basic status code | 550 |
| Description | The associated sender address has a null MX, and the SMTP receiver is configured to reject mail from such sender (e.g., because it could not return a DSN). |

## Dealing with Null MX records

Currently, MX records are automatically checked on delivery. If the destination server provides a NULL MX record, the message is immediately moved into the dead queue.

In future release, it will be possible to configure rules to check for null MX records using filtering and decide what to do with the email.