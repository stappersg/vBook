# Examples

## Personal MTA/MDA

### Context

A personnal MTA for Doe's family and small business.

Domain name : foo.bar
Users : john.doe@foo.bar, jane.doe@foo.bar, jimmy.doe@foo.bar, jenny.doe@foo.bar

### Network configuration

Doe's family has a router/firewall to route and secure their home network.
There's a small server in the DMZ to manage the family website, emails, etc. 

vSMTP is installed on an Ubuntu server 20.04 virtual instance.

```console
{ Internet ISP } --- Firewall --- { DMZ : MTA }
                        |
              { Internal Network }
```

- Public IP : 80.80.80.80
- DMZ MTA IP : 192.168.1.254/32
- Internal Network : 192.168.0.0/24

___Firewall rules___

```shell
# Pseudo code
#
# Allow SMTP and IMAP from Internet to MTA
Public IP > MTA : TCP/SMTP 25, TCP/SMTP 465
# Allow viewing family emails using IMAP/ssl from the Internet 
Public IP > MTA : IMAP/ssl 993 
# Outgoing SMTP traffic
Internal NET > MTA : TCP/SMTP 25, TCP/SMTP 465
MTA > {Internet} : TCP/SMTP 25, TCP/SMTP 465
# DNS traffic from MTA
MTA > {Internet} : UDP/DNS 53, TCP/DNS 53
```

___DNS___

```shell
MX preference = 1, mail exchanger = vsmtp.foo.bar
```

### vSMTP configuration


___object.vsl___

___main.vsl___

toto


