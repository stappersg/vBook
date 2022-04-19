# The vSL magic garden explained

> This is a v0.11 draft

vSL comes with many predefined functions allowing the user to use them directly or to adapt them to his needs. These functions can be found in the the standard addons folder `rules/addons/std/`.

Remember the SPF rule we added in the [step-by-step] tutorial. In the addons folder, there's a file `auth.vsl` that comes with functions dedicated to authentication methods. One is called `check_spf()`.

[step-by-step]: ../start/configuration/hardening.md



> Please refer to the [SPF chapter] for detailed information about SPF protocol.

[SPF chapter]: ./eam/spf.md

Let's browse the code together.

```javascript
//
// auth.vsl
//
// standard library for authentication
// 

import "addons/std/codes.vsl" as code;
```

_The SPF framework required specific return codes described in RFC 7372. vSL comes with predefined codes. You can use them in your own functions. Just import them from the `addons/std/codes.vsl` file._

```javascript
//
// Function check_spf(ctx) : SPF evaluation (RFC 7208)
// - return : deny() or next()
// - args : the message and the server contexts
//
//
// vsmtp.toml variables required : 
// - server.auth.spf.strict (boolean)
// - server.auth.spf.header (spf | auth | both | none)
//
// 
fn check_spf(ctx) {
```

_To access to the message structure (i.e. the HELO/EHLO string) we must pass the message context (ctx) in argument._

```javascript
    let query = vsl::check_spf(ctx.client_ip, ctx.mail_from, "");
```
_Wait... there are two functions check_spf ? Yes !_

_The predefined function `api::check_spf()` calls an internal vSL function `vsl::check_spf()`.
That means that you can either utilize the predefined function `api::check_spf()` or modify/create a new one that calls `vsl::check_spf()`._

```javascript
    // vsl::check_spf() : a wrapper for viaspf::evaluate_sender (viaspf crate)
    //
    // - return :
    //    * result : the result of an SPF evaluation.
    //      <string> <== Enum viaspf::SpfResult
    //
    //    * explanation : an explanation of why a query evaluated to a fail result (RFC 7208-6.2).
    //      <string> <== Enum viaspf::SpfResult { Fail(ExplanationString) }
    //                   Set to empty otherwise.
    //
    //    * cause : the "mechanism" that matched or the "problem" error (RFC 7208-9.1).
    //      <string> <== Enum viaspf::SpfResultCause
    //                   Set to "default" if no mechanisms matched w/o error
    //
    // - args : client ip, sender address, an optional helo/ehlo string.
    //          
    // - comments : HELO check is only performed when the HELO string is a valid domain name.
    //              
    // ISSUE: Identity checked (RFC 7208-9.1). identity= "mailfrom" / "helo" / "other" 
    //        Required to fill helo or envelope-from fields. Currently identity is forced to mailfrom
    //        by passing an empty string in the last argument.
    //        Check if it can be extract from viaspf::trace::Trace.
```

_You can find information about the function, the internal ones, etc. and even if there is a pending issue._

```javascript
    // Deny unwanted messages
    if toml::server.auth.spf.strict {
```

_This is the second big improvement of vSL: the vSMTP server configuration is directly available in vSL. In this case we need to retrieve the SPF policy field to choose to deny or to mark as SPAM a message in case of SPF policy failure._

```javascript
        switch query.result {
            "fail" => return vsl::deny(code::code550_7_23),
            "temperror" => return vsl::deny(code::code451_7_24),
            "permerror" => return vsl::deny(code::code550_7_24),
            _ => {},
        } 
```

_Here are the SMTP predefined codes we imported in line 1. With a strict SPF we deny the message and we send the corresponding SMTP code to the client. Otherwise we set modify the message by adding "JUNK:" in the subject._

```javascript
    } else { 
        // Add "JUNK:" in the subject
        if query.result != "pass" { 
            vsl::set_header(ctx, "Subject", "JUNK:" + get_header(ctx, "Subject"));
        }
    }
```

_Now the build the header using the objects (result, explanation and cause) returned by the vsl::check_spf() function._

```javascript
    // Record the result in a header (RFC 7208-9)
    let spf_header = query.result
        + if query.result == "fail" { ` ( ${query.explanation} )` } 
        + `\n receiver=${srv.hostname}; client-ip=${ctx.client_ip};`
        + `\n identity=mailfrom; envelope_from=${ctx.mail_from};`
        + if query.result == "pass" { `\n mechanism=${query.cause};` }
        + if (query.result == "temperror" || query.result == "permerror") { `\n problem=${query.cause};` };
        
    let auth_header = `${srv.hostname}; spf=${query.result}`
        + `\n reason=\" ${spf_header} \" smtp.mailfrom=${ctx.mail_from}`;
```

```javascript
    // The Received-SPF header field is a trace field 
    // and SHOULD be prepended to the existing header, above the Received: field 
    // It MUST appear above all other Received-SPF fields in the message.  
    switch toml::server.auth.spf.header {
```

_Again we have to check a TOML server variable to decide which kind of header will be added to the message._

```javascript
        "spf" => add_header(ctx, "Received-SPF", spf_header),  
        "auth" => add_header(ctx, "Authentication-Results", auth_header),
        "both" => {
            add_header(ctx, "Authentication-Results", auth_header),
            add_header(ctx, "Received-SPF", spf_header),
        // "None" is available but "it is RECOMMENDED that SMTP receivers record the result"
        "none" => {}, 
        _ => throw `From SPF Check : TOML field ${toml::server.auth.spf.header} unknown`,
    }

    return vsl::next();

}
```

Now you can edit your main.vsl code and add the check_spf function.

```javascript
// main.vsl
import "/addons/std/api" as api;

mail: [
  rule "check_spf" || api::check_spf(ctx);
]

// ...
```

Feel free to create your own addons and submit them on the dedicated [vSMTP addons] repository.

[vSMTP addons]: https://github.com/viridIT/vsl-addons
