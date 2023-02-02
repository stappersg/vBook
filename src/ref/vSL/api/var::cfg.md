# `app`

```rust
let app = #{
    "dirpath": "/var/spool/vsmtp/app",
    "logs": #{
        "filename": "/var/log/vsmtp/app.log",
    },
    "vsl": #{
        "domain_dir": (),
        "filter_path": (),
    },
}
```
# `server`

```rust
let server = #{
    "client_count_max": 16,
    "dns": #{
        "type": "system",
    },
    "interfaces": #{
        "addr": [
            "127.0.0.1:25",
        ],
        "addr_submission": [
            "127.0.0.1:587",
        ],
        "addr_submissions": [
            "127.0.0.1:465",
        ],
    },
    "logs": #{
        "filename": "/var/log/vsmtp/vsmtp.log",
        "level": [
            "warn",
        ],
        "system": (),
    },
    "message_size_limit": 10000000,
    "name": "deadass",
    "queues": #{
        "delivery": #{
            "channel_size": 32,
            "deferred_retry_max": 100,
            "deferred_retry_period": "5m",
        },
        "dirpath": "/var/spool/vsmtp",
        "working": #{
            "channel_size": 32,
        },
    },
    "smtp": #{
        "auth": (),
        "codes": #{
            "AlreadyUnderTls": "554 5.5.1 Error: TLS already active\r\n",
            "AuthClientCanceled": "501 Authentication canceled by client\r\n",
            "AuthClientMustNotStart": "501 5.7.0 Client must not start with this mechanism\r\n",
            "AuthErrorDecode64": "501 5.5.2 Invalid, not base64\r\n",
            "AuthInvalidCredentials": "535 5.7.8 Authentication credentials invalid\r\n",
            "AuthMechNotSupported": "504 5.5.4 Mechanism is not supported\r\n",
            "AuthMechanismMustBeEncrypted": "538 5.7.11 Encryption required for requested authentication mechanism\r\n",
            "AuthSucceeded": "235 2.7.0 Authentication succeeded\r\n",
            "AuthTempError": "454 4.7.0 Temporary authentication failure\r\n",
            "BadSequence": "503 Bad sequence of commands\r\n",
            "Closing": "221 Service closing transmission channel\r\n",
            "ConnectionMaxReached": "554 Cannot process connection, closing\r\n",
            "DataStart": "354 Start mail input; end with <CRLF>.<CRLF>\r\n",
            "Denied": "554 permanent problems with the remote server\r\n",
            "Failure": "451 Requested action aborted: local error in processing\r\n",
            "Greetings": "220 {name} Service ready\r\n",
            "Helo": "250 Ok\r\n",
            "Help": "214 joining us https://viridit.com/support\r\n",
            "MessageSizeExceeded": "552 4.3.1 Message size exceeds fixed maximum message size\r\n",
            "Ok": "250 Ok\r\n",
            "ParameterUnimplemented": "504 Command parameter not implemented\r\n",
            "SyntaxErrorParams": "501 Syntax error in parameters or arguments\r\n",
            "Timeout": "451 Timeout - closing connection\r\n",
            "TlsGoAhead": "220 TLS go ahead\r\n",
            "TlsNotAvailable": "454 TLS not available due to temporary reason\r\n",
            "TooManyError": "451 Too many errors from the client\r\n",
            "TooManyRecipients": "452 Requested action not taken: too many recipients\r\n",
            "Unimplemented": "502 Command not implemented\r\n",
            "UnrecognizedCommand": "500 Syntax error command unrecognized\r\n",
        },
        "error": #{
            "delay": "5s",
            "hard_count": 20,
            "soft_count": 10,
        },
        "rcpt_count_max": 1000,
        "timeout_client": #{
            "connect": "5m",
            "data": "5m",
            "helo": "5m",
            "mail_from": "5m",
            "rcpt_to": "5m",
        },
    },
    "system": #{
        "group": "vsmtp",
        "group_local": (),
        "thread_pool": #{
            "delivery": 6,
            "processing": 6,
            "receiver": 6,
        },
        "user": "vsmtp",
    },
    "tls": (),
    "virtual": #{},
}
```
