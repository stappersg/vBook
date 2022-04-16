# Step-by-step tutorial

In this tutorial we will follow Doe's family. John, Jane and their child Jimmy and Jenny want to self-host their mailboxes.

## Context

They have has a router/firewall to route and secure their home network and there is a small server in the DMZ to manage the family website, emails, etc.

The network looks like that :

```console
{ Internet ISP } --- Firewall --- { DMZ }
                        |
              { Internal Network }
```  

They also bought a domain name `doe-family.com`. They decided to prefixe their mailboxes with the common standard "first_name.last_name" like `jenny.doe@doe-family.com`

### Network configuration

vSMTP is installed on an Ubuntu server 20.04 virtual instance hosted by the DMZ server.

```console
{ Internet ISP } --- Firewall --- { DMZ : MTA }
                        |
              { Internal Network }


- Public IP : 80.80.80.80
- MTA IP : 192.168.1.254/32
- Internal Network : 192.168.0.0/24
```

___Firewall rules___

```shell
# Pseudo code - depends on your FW
#
# Allow SMTP and IMAP from Internet to MTA
Public IP > MTA : TCP/SMTP 25, TCP/SMTP 465, TCP/SMTP 587
# Allow viewing family emails using IMAP/ssl from the Internet 
Public IP > MTA : IMAP/ssl 993 
# Outgoing SMTP traffic
Internal NET > MTA : TCP/SMTP 25, TCP/SMTP 465, TCP/SMTP 587
MTA > {Internet} : TCP/SMTP 25, TCP/SMTP 465
# DNS traffic from MTA
MTA > {Internet} : UDP/DNS 53, TCP/DNS 53
```

___DNS___

```shell
MX preference = 1, mail exchanger = vsmtp.doe-family.com
```
