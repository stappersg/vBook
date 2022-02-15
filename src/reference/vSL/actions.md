# vSL predefined functions

vSL provides the user with a comprehensive list of predefined functions in order to interact with SMTP traffic. These functions are bounded to a namespace named `vsl`.

```rust,ignore
vsl::log(`Hello world !!!`, "/tmp/my_log");
```

## Rule engine actions

The state of an SMTP transaction can be changed through specific actions sent by the rule engine.

| Description | Syntax | Comment
| :--- | :--- | :---
| Accept | accept() | Skip rules in the current stage. Move to the next SMTP stage.
| Force accept | faccept() | Skip all rules and move the mail to the deliver queue.
| Continue processing | next() | Jump to the next rule or to the 1st rule of the next stage.
| Deny processing | deny() | Deny the mail and send a SMTP return code.
| Quarantine | quarantine(dir) | Skip all rules and move the mail to a quarantine queue in the specified directory.

## Actions over SMTP envelop and body

SMTP envelop can be modified by several predefined actions.

Syntax | Comment
| :--- | :---
| add_rcpt(addr) | Add addr to recipient list.
| remove_rcpt(addr) | Remove addr from recipient list.
| rewrite_rcpt(old, new) | Rewrite recipient "old" with "new".
| rewrite_helo(string) | Change HELO/EHLO string.
| rewrite_mail_from(addr) | Change MAIL FROM: current value with addr.
| parse() | Parse the mail and extract its structure including MIME parts.

&#9998; | Email headers "To:", "From:", "Reply-to:", etc. are also updated.
This apply only to the root headers in case of nested emails.

### Other actions

These actions have no impact on the SMTP engine.

Syntax | Description
| ---- | ---- |
| send_mail(from, to, path, relay) | Send an informative email
| bcc
| write(file) | Write a raw copy of the mail on disk.
| dump(file) | Write a copy of the entire mail (envelop+body) in JSON format on disk[^dump].
| log(string, file) | logs a message to stdout, stderr or a file.
| log_\<string>(string) | Log a message to a stream.

Streams can be :

- a Unix standard output : out (stdout) and err (stderr)
- a filter level of the logger (error, warn, info, debug, trace)

&#9998; | Target directories for log, write and dump are specified in the TOML configuration file.

user_exist ?????????????????????????????????????????

### Deliver actions

These specific actions are described in the [delivery] chapter.

[delivery]: delivery.md

### Chaining actions

```rust,ignore
{
    vsl::log(`Hello world !!!`, "./tmp/my_file");
    vsl::dump("./tmp/mail/dump/my_file");
}
```

### User-defined actions

Combined actions can be declared using a [RHAI](https://rhai.rs/) function. To access the actions defined by vSL (ACCEPT, DENY, etc.), the vsl context must be passed as a parameter.

```rust,ignore
fn my_faccept(vsl) {                              
    vsl::log("Hello world !!!", "/tmp/my_file");
    vsl::faccept()
    // Implicit return syntax, no trailing comma
    // equivalent to : return vsl::faccept();
}
```

Executing my_faccept will log the mail and send a FACCEPT action to the SMTP engine.