# Domain-based Message Authentication, Reporting and Conformance 

> ___This is a DRAFT for future releases. Support is planned for Q3/2022.___

This document specifies the vSMTP implementation of the Domain-based Message Authentication, Reporting and Conformance (DMARC) protocol described in [RFC 7489](https://www.rfc-editor.org/rfc/rfc7489.html).

DMARC allows email administrators to prevent hackers from impersonating their organization. This type of attack is also called "spoofing" because the message appears to come from the spoofed organization or domain.

> In order to counter spoofing attacks, DMARC uses SPF and DKIM protocols.

When a message appears to come from an organization, but does not pass authentication checks or does not meet the authentication criteria, DMARC policy tells mail servers what action to take.
