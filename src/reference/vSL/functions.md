# vSL predefined functions

vSL provides the user with a comprehensive list of predefined functions in order to interact with SMTP traffic.

## vSL context and namespace

vSL predefined functions are bounded to a namespace named `vsl`.

```c
vsl::accept();      
```

If the function performs actions on the email, the vSL context `ctx` must be passed as the first argument. However, the context can be omitted if the function has no argument or doesn't require it.

!!!!!!!!!!!! PARLER DU CONTEXTE SRV


```c
vsl::add_rcpt(ctx, "john.doe@mycompany.com");
vsl::log("warn", "Hello world !!!");   
```

## SMTP state changing functions

The state of an SMTP transaction can be changed through specific functions sent by the rule engine. They do not change the email context.

| Description |  syntax | Comment
| :--- | :--- | :---
| Accept | accept() | Skip rules in the current stage. Move to the next SMTP stage. (f.e. rcpt -> preq)
| Force accept | faccept() |Skip all rules and move the mail to the deliver queue.
| Continue processing | next() | Jump to the next rule or to the 1st rule of the next stage.
| Deny processing | deny() | Deny the mail and send a SMTP return code.
| Quarantine | quarantine(srv, ctx, path) | See hereunder.

### About quarantine function

The quarantine pushes the mail in a user defined quarantine directory.

The ENTIRE content of the email is written in JSON format regardless of the stage declared in the rule (including the envelop and body). All rules are skipped, and the server delivers a 554 smtp code to the client.

The root directory for quarantine() is specified in the TOML configuration file and the (path/file) is added.

```c
vsl::quarantine(srv, ctx, virus_dir);   
```

!!!!!!!! TO DO EXEMPLE QUARANTAINE avec un ACCEPT()

## SMTP envelop and body changing functions

SMTP envelop can be modified by several predefined actions. Thus they must include `ctx`as their first argument.

Syntax | Comment
| :--- | :---
| add_header(ctx, string) | Add a new header
| remove_header(ctx, string) | Remove all occurrences of headers matching the string.
| add_rcpt(ctx, addr) | Add addr to recipient list.
| remove_rcpt(ctx, addr) | Remove addr from recipient list.
| rewrite_rcpt(ctx, old, new) | Rewrite recipient "old" with "new".
| rewrite_mail_from(ctx, addr) | Change MAIL FROM: current value with addr.

&#9998; | Email headers "To:", "From:", "Reply-to:", etc. are also updated.
This apply only to the root headers in case of nested emails.

```c
vsl::remove_header(ctx, my_regex);   
```

## Deliver actions

These specific functions are described in the [delivery] chapter.

[delivery]: delivery.md

## Miscellaneous functions

These actions have no impact on the SMTP engine.

Syntax | Description
| ---- | ---- |
| bcc(ctx, addr) | Send a blind carbon copy of the mail.
| write(ctx, file) | Write a raw copy of the mail on disk[^dir].
| dump(ctx, file) | Write a copy of the entire mail (envelop+body) in JSON format[^dump] on disk[^dir].
| body_parse() | Parse the mail and extract its structure including MIME parts.
| send_mail(from, to, path, relay) | Send an informative email.
| log(loglevel, msg) | logs a message[^log].
| user_exist(string) | Check if an user exists locally.

[^dir]: Root directories for write and dump are specified in the TOML configuration file.
[^log]: Log files and log levels are described in the TOML configuration file.

```rust,ignore
vsl::log("warn", `Hello world !!!`);
```

### About the dump function

This function dumps in JSON format only the available content at a stage.  The body still in raw mode if the parsing has not been performed. The filename is the `message id` of the email.

## Chaining actions

```rust,ignore
{
    vsl::log("info", "Hello world !!!");
    vsl::dump("./tmp/mail/dump/my_file");
}
```

## User-defined actions

Combined actions can be declared using a [RHAI](https://rhai.rs/) function.

```rust,ignore
fn my_faccept() {                              
    vsl::log("info", "Hello world !!!");
    vsl::faccept()
    // Implicit return syntax, no trailing comma
    // equivalent to : return vsl::faccept();
}

// functions in vsl are "pure" (black-boxes), this means that you must
// pass necessary variables as parameters. (here, 'ctx' to remove john from
// the recipient list)
fn my_custom_action(ctx) {
    vsl::remove_rcpt(ctx, "john.doe@mycompany.com");
    vsl::next()
}

// execute your functions.
my_faccept();
my_custom_action(ctx);
```

Executing `my_faccept` will log `Hello world !!!` and send a FACCEPT status to the SMTP engine.
Executing `my_custom_action` will log remove john from rcpt and tells the rule engine to proceed to the next rule / action.
