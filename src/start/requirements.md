# Requirements

vSMTP is a stand-alone application with few kernel interactions, it may run on any system with slight modifications.

> vSMTP is currently under development. There's only a DEBIAN package. Anyway vSMTP can be easily compiled from source code.

## Physical requirements

The current release has been tested on x86/64 environments. Installing vSMTP on other CPU architectures like ARM should work but may require specific configurations not covered in this document.

## Operating systems

Although vSMTP is developed and tested on Ubuntu Server 20.04 with kernel 5.4, all recent Linux distributions should be able to run vSMTP.

FreeBSD 13.x is supported using the latest port branch which includes Rust 1.58.
NetBSD and OpenBSD supports are planned for Q3-2022.

Microsoft Windows Server is not supported.

## Software requirements

vSMTP is a Mail Transfer Agent (MTA) and is not intended to be a Mail User Agent (MUA) or a Mail Delivery Agent (MDA).

For outgoing mail, your email client (MUA) can directly address vSMTP using the SMTP protocol. For incoming mails, vSMTP can deliver local mail to a client storage using mbox or maildir formats. In order to retrieve emails from your preferred mail reader (MUA) it is necessary to install a MDA that can handle POP and/or IMAP protocols.

&#9758; | For Debian/Ubuntu server the most straightforward solution is to download and install [courier-imap] package and specify to the courier-imap MDA where are located the MailDir/ folders and use a MUA like Mozilla ThunderBird.

[courier-imap]: https://packages.debian.org/search?keywords=courier-imap
