# Features

## Connection

- [x] v0.7 Support ipv4 and ipv6 address
- [x] v0.7 Handling concurrently multiple connection
- [x] v0.7 Handle multiple mail for each connection
- [x] v0.7 Minimal implementation of the rfc 5321 (Simple Mail Transfer Protocol) and (Internet Message Format)
- [x] v0.7 Opportunistic and required TLS upgrade (STARTTLS mechanism)

## API

- [x] v0.7 Application logs
- [x] v0.7 Mail exportable in raw and json

## Filtering

- [x] v0.8 Post queue filtering
- [x] v0.7 Rules definable in the state: HELO/EHLO, CONNECT, MAIL, RCPT, DATA, PREQ
- [x] v0.7 Simple action: ACCEPT, FACCEPT, DENY, LOG

## Delivery

- [x] v0.8 MTA remote devilivery (SMTP)
- [x] v0.8 Local Unix delivery using "mbox"  protocol
- [x] v0.7 Local delivery using "maildir" (IMAP) protocol
