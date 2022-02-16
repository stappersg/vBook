# vSL predefined functions

vSL provides the user with a comprehensive list of predefined functions in order to interact with SMTP traffic. 

## vSL context and namespace

vSL predefined functions are bounded to a namespace named `vsl`. 

```rust,ignore
vsl::accept();      
```

If the function performs actions on the email, the vSL context `ctx` must be passed as the first argument.

```rust,ignore
vsl::add_rcpt(ctx, `john.doe@mycompany.com`);
```

The context can be omitted if the function has no argument or if the function doesn't require it.

```rust,ignore
vsl::log(`Hello world !!!`, "/tmp/my_log");   
```

## SMTP state changing functions

The state of an SMTP transaction can be changed through specific functions sent by the rule engine. They do not change the email context.

```rust,ignore
vsl::quarantine(virus_dir);   
```

| Description |  syntax | Comment
| :--- | :--- | :---
| Accept | accept() | Skip rules in the current stage. Move to the next SMTP stage.
| Force accept | faccept() |Skip all rules and move the mail to the deliver queue.
| Continue processing | next() | Jump to the next rule or to the 1st rule of the next stage.
| Deny processing | deny() | Deny the mail and send a SMTP return code.
| Quarantine | quarantine(path/file) | Skip all rules and move the mail to a quarantine queue in the specified directory. The (path/file) is appended to the TOML quarantine_dir.

## SMTP envelop and body changing functions

SMTP envelop can be modified by several predefined actions. Thus they must include `ctx`as their first argument.

```rust,ignore
vsl::remove_header(ctx, my_regex);   
```

Syntax | Comment
| :--- | :---
| add_header(ctx, string) | Add a new header
| remove_header(ctx, regex) | Remove all occurrences of headers matching the regex.
| add_rcpt(ctx, addr) | Add addr to recipient list.
| remove_rcpt(ctx, addr) | Remove addr from recipient list.
| rewrite_rcpt(ctx, old, new) | Rewrite recipient "old" with "new".
| rewrite_mail_from(ctx, addr) | Change MAIL FROM: current value with addr.

&#9998; | Email headers "To:", "From:", "Reply-to:", etc. are also updated.
This apply only to the root headers in case of nested emails.

## Miscellaneous functions

These actions have no impact on the SMTP engine.

Syntax | Description
| ---- | ---- |
| bcc(ctx, addr) | Send a blind carbon copy of the mail
| write(ctx, file) | Write a raw copy of the mail on disk.
| dump(ctx, file) | Write a copy of the entire mail (envelop+body) in JSON format on disk[^dump].
| parse() | Parse the mail and extract its structure including MIME parts.
| send_mail(from, to, path, relay) | Send an informative email
| log(string, file) | logs a message to stdout, stderr or a file.
| log_\<stream>(string) | Log a message to a stream[^stream].

[^stream]: Streams can be a Unix standard output : out (stdout) and err (stderr) or a log level (error, warn, info, debug, trace).

```rust,ignore
vsl::log_warn(`Hello world !!!`);
```


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

Combined actions can be declared using a [RHAI](https://rhai.rs/) function. 

```rust,ignore
fn my_faccept() {                              
    vsl::log("Hello world !!!", "/tmp/my_file");
    vsl::faccept()
    // Implicit return syntax, no trailing comma
    // equivalent to : return vsl::faccept();
}
```

Executing my_faccept will log the mail and send a FACCEPT action to the SMTP engine.