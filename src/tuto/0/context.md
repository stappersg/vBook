# Context

They use a router/firewall to route and secure their home network. They also setup a small server in the DMZ to manage the family website, emails, etc.

```console
{ Internet ISP } --- Firewall --- { DMZ }
                        |
              { Internal Network }
```
<p class="ann"> Does family network setup </p>

They also rented a domain name `doe-family.com`. They decided to prefix their mailboxes with the common standard "first_name.last_name" like `jenny.doe@doe-family.com`

## Network configuration

vSMTP is installed on an Ubuntu server 20.04 virtual instance hosted by the DMZ server.

```console
{ Internet ISP } --- Firewall --- { DMZ : MTA }
                        |
              { Internal Network }


- Public IP : 80.80.80.80
- MTA IP : 192.168.1.254/32 - fqdn : mta.doe-family.com
- Internal Network : 192.168.0.0/24
```
<p class="ann"> Network setup </p>

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
<p class="ann"> Firewall rules </p>

```shell
MX preference = 1, mail exchanger = vsmtp.doe-family.com
```
<p class="ann"> DNS setup </p>

John generated a certificate through the [Let's Encrypt Certificate Authority](https://letsencrypt.org/) for vSMTP server.

```shell
sudo certbot certonly --manual --preferred-challenges=dns \
    --agree-tos -d mta.doe-family.com
```
<p class="ann"> Creating the certificate </p>
