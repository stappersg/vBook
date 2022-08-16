# Email Authentication Mechanisms

Prevent scammers from usurping an identity by using its domain name is a must nowadays.  This is where the SPF, DKIM and DMARC authentication protocols come into play.

This chapter described how to define vSMTP as a legitimate sender and receiver.

## SPF and DKIM : what's that all about ?

Sender Policy Framework (SPF) specifies the authorized senders in a given domain. It thus allows email clients to check that incoming email from a domain comes from a host authorized by the administrator of this domain.

> SPF is an authentication standard that links a domain name and an email address.

The DomainKeys Identified Mail (DKIM) protocol allows the sender to sign its message with its domain name. The DKIM protocol is used to attest that the domain name has not been usurped, and that the message has not been altered during its transmission.

> DKIM is an authentication protocol that links a domain name to a message.

The simultaneous use of this two protocols is one of the most effective way to prevent phishers and other fraudsters from impersonating a legitimate sender using its domain name.

The implementation of these protocols improves email deliverability, since senders are better identified by the ISPs (Internet Service Providers) and email clients of your recipients. You then optimize your chances that your emails will 

These two protocols are now widely used. A message sent without an SPF and/or DKIM signature is viewed with suspicion by the various email analysis tools and may be flagged as a “spam”.

## SPF and DKIM : limitations

SPF has limits. If a message is forwarded, the verification may not be performed, since the address of the sender of the forwarded message is not necessarily included in the list of addresses agreed by the SPF evaluation.

DKIM also has limits. The DKIM signature does not prevent the sender from being considered a spammer if good emailing practices are not applied.

Moreover, SPF and DKIM do not specify the action to apply in case of verification failure. The DMARC protocol comes in, tells the recipient's server how it should act if the sender's authentication processes fail.

## DMARC standard

Domain-based Message Authentication, Reporting and Conformance, or DMARC, is an authentication standard complementary to SPF and DKIM intended to fight more efficiently against phishing and other spamming practices.

> DMARC allows domain holders to tell ISPs and email clients what to do when a signed message from their domain is not formally identified by a SPF or a DKIM mechanism.

## ARC (extension to DMARC)

Parts of legitimate messages (subject tags, footers, etc.) can be altered due to forwarding (mailing list, virus scanner, etc.) and thus no longer succeed commonly accepted authentication checks. It can happen when an Internet domain publishes a strict DMARC policy.

>ARC captures and conveys authentication results and allows the final recipient to check the authentication status of the message when it arrives at the first ARC-aware MTA.

## BIMI

Brand Indicators for Message Identification (BIMI) is a future standard that makes it easier to identify the sender of an email. BIMI coordinates e-mail publishers and domain name owners to allow the latter to display their logos directly at the level of their customers' e-mail boxes, i.e. next to the name of the issuer. BIMI requires DMARC.

> For brands, BIMI is an opportunity to protect their identities by e-mail (fight against "phishing") and to increase the reach and visibility of their logos. Because these logos are only included in DMARC-authenticated emails, consumers' trust in their brands is also enhanced.
