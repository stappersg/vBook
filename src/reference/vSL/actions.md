# Actions

vSL provides the user with a comprehensive list of predefined actions in order to interact with mail traffic.

```vsl
vsl.LOG(`Hello world !!!`, "/tmp/my_log");
```

## Rule engine actions

The state of an SMTP transaction can be changed through specific actions sent by the rule engine.

| Action | Description | Syntax | Comment
| :--- | :--- | :--- | :---
| ACCEPT | Accept | ACCEPT() | Skip rules in the current stage. Move to the next SMTP stage (1).
| FACCEPT | Force accept | FACCEPT() | Skip all rules and move the mail to the deliver queue.
| CONTINUE | Continue processing | CONTINUE() | Jump to the next rule or to the 1st rule of the next stage. (2)
| DENY | Deny processing | DENY() | Deny the mail and send a SMTP return code.
| BLOCK | Quarantine | BLOCK(dir) | Skip all rules and move the mail to a quarantine queue in the specified directory.

>(1) Except for the RCPT stage. See "advanced scripting".
>(2) See Rules implicit behavior.

## Actions over SMTP envelop

SMTP envelop can be modified by several predefined actions.

| Action | Syntax | Description
| :--- | :--- | :---
| ADD_RCPT | ADD_RCPT(addr) | Add addr to recipient list.
| DEL_RCPT | DEL_RCPT(addr) | Remove addr from recipient list.
| RW_RCPT | RW_RCPT(addr) | Change RCPT TO: current value with addr.
| RW_HELO | RW_HELO(string) | Change HELO/EHLO string.
| RW_MAIL | RW_MAIL(addr) | Change MAIL FROM: current value with addr.

>Please note that the email body is not modified.
>Modification of headers "To:", "From:", "Reply-to:", etc. are not implemented in version 0.7.x.

## Other actions

These actions have no impact on the SMTP engine.

| Action | Syntax | Description |
| ---- | ---- | ---- |
| LOG | LOG(string, file) | Log to a file. |
| LOG_ERR | LOG_ERR(string) | Print a message on stderr. |
| LOG_OUT | LOG_OUT(string) | Print a message on stderr. |
| WRITE | WRITE(file) | Write a raw copy of the mail on disk. |
| DUMP | DUMP(file) | Write a copy of the entire mail (envelop+body) in JSON format on disk. |

## Combining and interacting with actions

### Chaining actions

```vsl
{
    vsl.LOG(`Hello world !!!`, "/tmp/my_file");
    vsl.DUMP("/tmp/mail/dump/my_file");
}
```

### User-defined actions

Combined actions can be declared using a [RHAI](https://rhai.rs/) function.

```vsl
fn my_faccept() {
    vsl.LOG("Hello world !!!", "/tmp/my_file");
    return vsl.FACCEPT();
}
```

Executing my_faccept will log the mail and send a FACCEPT action to the SMTP engine.

```vsl
fn my_faccept() {
    vsl.LOG("Hello world !!!", "/tmp/my_file");
    vsl.FACCEPT()
}
```

>Please note the implicit return syntax (no comma).
