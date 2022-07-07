# Mail Agent

## MUA (Mail User Agent)

Client application that allows receiving and sending emails. It can be a desktop application such as Microsoft Outlook/Thunderbird/… or web-based such as Gmail/Hotmail/… (the latter is also called Webmail).

## MSA (Mail Submission Agent)

A server program that receives mail from an MUA, checks for any errors, and transfers it (with SMTP) to the MTA hosted on the same server.

## MTA (Mail Transfer Agent)

A server application that receives mail from the MSA, or from another MTA. It will find (through name servers and the DNS) the MX record from the recipient domain's DNS zone in order to know how to transfer the mail. It then transfers the mail (with SMTP) to another MTA (which is known as SMTP relaying) or, if the recipient’s server has been reached, to the MDA.

## MDA (Mail Delivery Agent)

A server program that receives mail from the server’s MTA, and stores it into the mailbox. MDA is also known as LDA (Local Delivery Agent).

An example is Dovecot, which is mainly a POP3 and IMAP server allowing an MUA to retrieve mail, but also includes an MDA which takes mail from an MTA and delivers it to the server’s mailbox.
