# Domain-based Message Authentication, Reporting and Conformance

This document specifies the vSMTP implementation of the Domain-based Message Authentication, Reporting and Conformance (DMARC) protocol described in [RFC 7489](https://www.rfc-editor.org/rfc/rfc7489.html).

DMARC allows email administrators to prevent hackers from impersonating their organization. This type of attack is also called "spoofing" because the message appears to come from the spoofed organization or domain.

> In order to counter spoofing attacks, DMARC uses SPF and DKIM protocols.

When a message appears to come from an organization, but does not pass authentication checks or does not meet the authentication criteria, DMARC policy tells mail servers what action to perform.

The DMARC implementation of vSMTP support the `Mail Receiver` part, and apply the policy specified in the DNS record.

This rule will  conducts SPF and DKIM authentication checks by passing the necessary data to their respective modules. The results of these are passed to the DMARC module along with the Author's domain.  The DMARC module attempts to retrieve a policy from the DNS for that domain. If a policy is found, it is combined with the Author's domain and the SPF and DKIM results to produce a DMARC policy result ("pass" or "fail").

```js
#{
  preq: [
    rule "check dmarc" || check_dmarc(),
  ]
}
```

DMARC reporting and DMARC feedback system is not implemented.