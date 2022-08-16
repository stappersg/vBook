# Null MX record

The "null MX" protocol is used to state that mail services are disable in a given domain. The protocol is described in [RFC 7505].

[RFC 7505]: https://www.rfc-editor.org/rfc/rfc7505.html

When a specific DNS record (a null MX) is effectively defined in the DNS zone of a given domain, all mail delivery attempts fail immediately.

## DNS record

The `null MX` RR is an ordinary MX record with an RDATA section consisting of preference number 0 and a "." as the exchange domain, to denote that there exists no mail exchanger.  

```dns
nomail.example.com. 86400 IN MX 0 "."
```

A domain that advertises a null MX __must not__ advertise any other MX RR.

## Sender with "Null MX" records

As Null MX is primarily intended for domains that do not send or receive any mail, vSMTP default behavior rejects mail that has an invalid return address.

Mail systems should not publish a null MX record for domains that they use in `MAIL FROM` (RFC5321) or `From` (RFC5322) directives.

## Null MX return codes

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


### vSL predefined functions

> ___This is a DRAFT for v1.2 features___

The standard API includes a dedicated abstract to check the Null MX record.

```javascript
// -- main.vsl

mail: [
  rule "check null MX" || check_null_mx();
]
```

> ___Current Behavior___

Currently, MX records are automatically checked on delivery. If the destination server provides a NULL MX record, the message is immediately moved into the dead queue.