# Email Authentication Mechanisms

Preventing scammers from usurping your identity by using your domain name is a must nowadays.  This is where the SPF, DKIM and DMARC authentication protocols come into play.

This chapter described how to define vSMTP as a legitimate sender and receiver.

## SPF and DKIM : what's that all about ?

Sender Policy Framework (SPF) consists of defining authorized senders in a given domain. It thus allows email clients to verify that incoming email from a domain comes from a host authorized by the administrator of this domain.

> SPF is an authentication standard for linking a domain name and an email address.

The DomainKeys Identified Mail (DKIM) protocol allows you to sign your email with your domain name. The objective of the DKIM protocol is not only to prove that the domain name has not been usurped, but also that the message has not been altered during its transmission.

> DKIM is an authentication protocol that links a domain name to a message.

These are the main protocols for verifying the identity of senders. This is one of the most effective ways to prevent phishers and other fraudsters from impersonating a legitimate sender whose identity they are impersonating using the same domain name.

The implementation of these protocols improves the deliverability of emails sent, since you will be better identified by the ISPs (Internet Service Providers) and email clients of your recipients. You then optimize your chances that your emails will arrive in the inbox of your recipients and not in the “spam” or “junk mail” folder.

These protocols have become standards for sending email. A message sent without an SPF and/or DKIM signature is viewed with suspicion by the various email analysis tools.

## SPF and DKIM : limitations

SPF has its limits. If the email is forwarded, the verification may not take place, since the address sending the forwarded message will not necessarily be included in the list of addresses validated by SPF.

As a sender, the DKIM signature will not prevent you from being considered a spammer if you do not apply good emailing practices.

Moreover, SPF and DKIM do not specify the action to apply in case of verification failure. This is where the DMARC protocol comes in, telling the recipient's server how it should act if the sender's authentication processes fail.

## DMARC standard

Domain-based Message Authentication, Reporting and Conformance, or DMARC, is an authentication standard complementary to SPF and DKIM intended to fight more effectively against phishing and other spamming practices.

> DMARC allows domain holders to tell ISPs and email clients what to do when a signed message from their domain is not formally identified by an SPF or DKIM standard.

## ARC (extension to DMARC)

Parts of legitimate messages (subject tags, footers, etc.) can be altered due to forwarding (mailing list, virus scanner, etc.) and thus no longer pass commonly accepted authentication checks. This can happen when an Internet domain publishes a strict DMARC policy.

>ARC captures and conveys authentication results and allows the final recipient to check the authentication status of the message when it arrived at the first ARC-aware MTA.

## BIMI

Brand Indicators for Message Identification, or BIMI is a future standard that makes it easier to identify the sender of an email. BIMI coordinates e-mail publishers and domain name owners to allow the latter to display their logos directly at the level of their customers' e-mail boxes, i.e. next to the name of the issuer. BIMI requires DMARC.

> For brands, BIMI is an opportunity to protect their identities by e-mail (fight against "phishing") and to increase the reach and visibility of their logos. Because these logos are only included in DMARC-authenticated emails, consumers' trust in their brands is also enhanced.
