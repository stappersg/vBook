# Requirements

## Physical requirements

The current release has been tested on x86/64 environments.
> Installing vSMTP on other CPU architectures should work but may require specific configurations not covered in this document.

## Operating systems

vSMTP is developed and tested on Ubuntu 20.04 server.
As it is a stand-alone application with no kernel interaction, it may run on any Linux system with slight modifications.

> FreeBSD and NetBSD supports are planned for mid 2022.

## Software requirements

vSMTP is a Mail Transfer Agent (MTA) and is not intended to be a Mail User Agent (MUA) or a Mail Delivery Agent (MDA).

For outgoing mail, vSMTP can directly be addressed by your email client (MUA) using the SMTP protocol. For incoming mails, vSMTP can deliver local mail to a client storage using mbox or maildir formats. In order to retrieve emails from your preferred mail reader (MUA) it is necessary to install a MDA that can handle POP and/or IMAP protocols.

For Debian/Ubuntu server the most straightforward solution is to download and install [courier-imap](https://packages.debian.org/search?keywords=courier-imap) package and specify to the courier-imap MDA where are located the MailDir/ folders.