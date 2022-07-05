# vSL predefined functions

vSL provides the user with a comprehensive list of predefined functions in order to interact with SMTP traffic.

## SMTP state changing functions

The state of an SMTP transaction can be changed through specific functions sent by the rule engine. They do not change the email context.

| Description         | syntax           | Comment                                                                           |
| :------------------ | :--------------- | :-------------------------------------------------------------------------------- |
| Accept              | accept()         | Skip rules in the current stage. Move to the next SMTP stage. (f.e. rcpt -> preq) |
| Force accept        | faccept()        | Skip all rules and move the mail to the deliver queue.                            |
| Continue processing | next()           | Jump to the next rule or to the 1st rule of the next stage.                       |
| Deny processing     | deny()           | Deny the mail and send a SMTP return code.                                        |
| Quarantine          | quarantine(path) | See hereunder.                                                                    |

### About quarantine function

The quarantine pushes the mail in a user defined quarantine directory.

The ENTIRE content of the email is written in JSON format regardless of the stage declared in the rule (including the envelop and body). All rules are skipped, and the server delivers a 250 smtp code to the client.

The root directory for `quarantine()` is specified in the TOML configuration file under `[app.dirpath]`.

```js
quarantine(virus_dir);
```

## SMTP envelop and body changing functions

SMTP envelop can be modified by several predefined actions.

| Syntax                                        | Comment                                                                    |
| :-------------------------------------------- | :------------------------------------------------------------------------- |
| append_header(name:string, body:string)       | Append a new header to the email's header section.                         |
| prepend_header(name:string, body:string)      | Prepend a new header to the email's header section.                        |
| remove_header(name:string)                    | Remove all occurrences of headers matching the string in the email's body. |
| rewrite_mail_from(address:string)             | Change `MAIL FROM:` current value with addr.                               |
| add_rcpt(address:string)                      | Add rcpt to the envelop.                                                   |
| remove_rcpt(address:string)                   | Remove rcpt from the envelop.                                              |
| rewrite_rcpt(old:string, new::string)         | Rewrite rcpt "old" with "new" in the envelop.                              |
| add_to(address:string)                        | Add rcpt to the `To` header in the email's body.                           |
| remove_to(address:string)                     | Remove rcpt from the `To` header in the email's body.                      |
| rewrite_to(old:string, new:string)            | Rewrite rcpt "old" with "new" from the `To` header in the email's body     |

&#9998; | `add_to`, `remove_to` & `rewrite_to` only update the root headers (nested emails headers are not changed).

```js
remove_header(my_regex);   
```

## Deliver actions

These specific functions are described in the [delivery] chapter.

[delivery]: delivery.md

## Miscellaneous functions

These actions have no impact on the SMTP engine.

| Syntax                           | Description                                                                         |
| -------------------------------- | ----------------------------------------------------------------------------------- |
| bcc(addr)                        | Send a blind carbon copy of the mail.                                               |
| write(file)                      | Write a raw copy of the mail on disk[^dir].                                         |
| dump(file)                       | Write a copy of the entire mail (envelop+body) in JSON format[^dump] on disk[^dir]. |
| send_mail(from, to, path, relay) | Send an informative email.                                                          |
| log(log-level, msg)              | logs a message[^log].                                                               |
| user_exist(string)               | Check if an user exists locally.                                                    |

[^dir]: Root directories for write and dump are specified in the TOML configuration file.
[^log]: Log files and log levels are described in the TOML configuration file.

```javascript,ignore
log("warn", "Hello world!");
```

### About the dump function

This function dumps in JSON format only the available content at a stage.  The body still in raw mode if the parsing has not been performed. The filename is the `message id` of the email.

## Chaining actions

```javascript,ignore
{
    log("info", "Hello world !!!");
    dump("./tmp/mail/dump/my_file");
}
```

## User-defined actions

Combined actions can be declared using a [RHAI](https://rhai.rs/) function.

```javascript
fn my_faccept() {                              
    log("info", "Hello world !!!");
    faccept()
    // Implicit return syntax.
    // equivalent to : return faccept();
}

// the recipient list)
fn my_custom_action() {
    remove_rcpt("john.doe@mycompany.com");
    next()
}

// execute your functions.
#{
    mail: [
            // the return value of my_custom_action (next)
            // is also returned by the "faccept" rule,
            // telling the server to read the next rule.
            rule "faccept" || my_custom_action(),
    ],

    preq: [
            // my_faccept returns faccept, thus telling the rule
            // engine to accept everything at this point without
            // evaluating other rules.
            rule "faccept" || my_faccept(),
    ],
}
```

Executing `my_custom_action` will log remove john from rcpt and tells the rule engine to proceed to the next rule / action.
Executing `my_faccept` will log `Hello world !!!` and send a FACCEPT status to the SMTP engine.