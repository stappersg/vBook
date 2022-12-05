# `code451_7_24`

```rust
let code451_7_24 = Code(
    Reply {
        code: Enhanced {
            code: 451,
            enhanced: "5.7.24",
        },
        text: "SPF validation error",
    },
)
```
# `code550_7_20`

```rust
let code550_7_20 = Code(
    Reply {
        code: Enhanced {
            code: 550,
            enhanced: "5.7.20",
        },
        text: "No passing DKIM signature found",
    },
)
```
# `code550_7_21`

```rust
let code550_7_21 = Code(
    Reply {
        code: Enhanced {
            code: 550,
            enhanced: "5.7.21",
        },
        text: "No acceptable DKIM signature found",
    },
)
```
# `code550_7_22`

```rust
let code550_7_22 = Code(
    Reply {
        code: Enhanced {
            code: 550,
            enhanced: "5.7.22",
        },
        text: "No valid author-matched DKIM signature found",
    },
)
```
# `code550_7_23`

```rust
let code550_7_23 = Code(
    Reply {
        code: Enhanced {
            code: 550,
            enhanced: "5.7.23",
        },
        text: "SPF validation failed",
    },
)
```
# `code550_7_24`

```rust
let code550_7_24 = Code(
    Reply {
        code: Enhanced {
            code: 550,
            enhanced: "5.7.24",
        },
        text: "SPF validation error",
    },
)
```
# `code550_7_25`

```rust
let code550_7_25 = Code(
    Reply {
        code: Enhanced {
            code: 550,
            enhanced: "5.7.25",
        },
        text: "Reverse DNS validation failed",
    },
)
```
# `code550_7_26`

```rust
let code550_7_26 = Code(
    Reply {
        code: Enhanced {
            code: 500,
            enhanced: "5.7.26",
        },
        text: "Multiple authentication checks failed",
    },
)
```
# `code550_7_27`

```rust
let code550_7_27 = Code(
    Reply {
        code: Enhanced {
            code: 550,
            enhanced: "5.7.27",
        },
        text: "Sender address has null MX",
    },
)
```
# `code554_7_1`

```rust
let code554_7_1 = Code(
    Reply {
        code: Enhanced {
            code: 554,
            enhanced: "5.7.1",
        },
        text: "Relay access denied",
    },
)
```
# `code556_1_10`

```rust
let code556_1_10 = Code(
    Reply {
        code: Enhanced {
            code: 556,
            enhanced: "5.1.10",
        },
        text: "Recipient address has null MX",
    },
)
```
# `code_greylist`

```rust
let code_greylist = Code(
    Reply {
        code: Enhanced {
            code: 451,
            enhanced: "4.7.1",
        },
        text: "Sender is not authorized. Please try again.",
    },
)
```
# `code_multi_destination`

```rust
let code_multi_destination = Code(
    Reply {
        code: Enhanced {
            code: 451,
            enhanced: "4.3.0",
        },
        text: "Multiple destination domains per transaction is unsupported. Please try again.",
    },
)
```
# `code_unknown_account`

```rust
let code_unknown_account = Code(
    Reply {
        code: Enhanced {
            code: 550,
            enhanced: "5.1.1",
        },
        text: "The email account that you tried to reach does not exist. Please try again.",
    },
)
```
# `net_10`

```rust
let net_10 = Rg4(
    IpRange [10.0.0.0/8],
)
```
# `net_172`

```rust
let net_172 = Rg4(
    IpRange [172.16.0.0/12],
)
```
# `net_192`

```rust
let net_192 = Rg4(
    IpRange [192.168.0.0/16],
)
```
# `non_routable_net`

```rust
let non_routable_net = [Rg4(
    IpRange [192.168.0.0/16],
), Rg4(
    IpRange [172.16.0.0/12],
), Rg4(
    IpRange [10.0.0.0/8],
)]
```
