# The vSL magic garden explained

> This is a v0.11 draft

vSL comes with many predefined function allowing the user to use them directly or to adapt them to his needs. These functions can be found in the the standard addons folder `rules/addons/std/`.

Remember the SPF rule we added in the [step-by-step] tutorial.

[step-by-step]: start/configuration/hardening.md

In this folder, there's a file `auth.vsl` that comes with functions dedicated to authentication methods. One is called `check_spf()`.

Let's browse the code together.

```javascript
/**
 * vSMTP mail transfer agent
 * Copyright (C) 2022 viridIT SAS
 *
 * This program is free software: you can redistribute it and/or modify it under
 * the terms of the GNU General Public License as published by the Free Software
 * Foundation, either version 3 of the License, or any later version.
 *
 *  This program is distributed in the hope that it will be useful, but WITHOUT
 * ANY WARRANTY; without even the implied warranty of MERCHANTABILITY or FITNESS
 * FOR A PARTICULAR PURPOSE.  See the GNU General Public License for more details.
 *
 * You should have received a copy of the GNU General Public License along with
 * this program. If not, see https://www.gnu.org/licenses/.
 *
**/

//
// auth.vsl
//
// standard library for authentication
// 

import "addons/std/codes.vsl" as code;

//
// Function check_spf() : SPF evaluation (RFC 7208)
// - return : deny() or next()
// - args : the message context
//
//
// vsmtp.toml variables required : 
// - server.hostname (string)
// - server.auth.spf.strict (boolean)
// - server.auth.spf.header (spf | auth | both | none)
//
// 
fn check_spf(ctx) {

    let query = vsl::check_spf(ctx.client_ip, ctx.mail_from, "");
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

    // Deny unwanted messages
    if toml::server.auth.spf.strict {
        switch query.result {
            "fail" => return vsl::deny(code::code550_7_23),
            "temperror" => return vsl::deny(code::code451_7_24),
            "permerror" => return vsl::deny(code::code550_7_24),
            _ => {},
        } 
    } else { 
        // Add "JUNK:" in the subject
        if query.result != "pass" { vsl::set_header(ctx, "JUNK:" + get_header(ctx, "Subject")) }
    }

    // Record the result in a header (RFC 7208-9)
    let spf_header = query.result
        + if query.result == "fail" { ` ( ${query.explanation} )` } 
        + `\n receiver=${toml::server.hostname}; client-ip=${ctx.client_ip};`
        + `\n identity=mailfrom; envelope_from=${ctx.mail_from};`
        + if query.result == "pass" { `\n mechanism=${query.cause};` }
        + if (query.result == "temperror" || query.result == "permerror") { `\n problem=${query.cause};` };
        
    let auth_header = `${toml::server.hostname}; spf=${query.result}`
        + `\n reason=\" ${spf_header} \" smtp.mailfrom=${ctx.mail_from}`;

    // The Received-SPF header field is a trace field 
    // and SHOULD be prepended to the existing header, above the Received: field 
    // It MUST appear above all other Received-SPF fields in the message.  
    switch toml::server.auth.spf.header {
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

Wait... there are two functions check_spf ? Yes !

The predefined function `api::check_spf()` calls an internal vSL function `vsl::check_spf()`.
That means that you can either utilize the predefined function `api::check_spf()` or modify/create a new one that calls `vsl::check_spf()`.

Sorry but I've got an other question: what is `toml::server.eam.spf_header` ? That's the second big improvement of vSL. You can access to the whole configuration using toml:: namespace.

To make it works you have to add in the vsmtp.toml file the table:

```toml
[server]
# hostname = "mta-01.example.com" // default = `hostname --fqdn`

[server.auth.spf]
TO DO
```

Again there are some predefined SMTP codes. You can find them in the codes.vsl file.

```javascript
// /addons/std/codes.vsl

// ... TO DO

object code mycode1 {
  number: 451
  enhanced: 4.4.2
  message: "mlkfmùlkjdfsùmsfdkj ùmfdlk  fdùmkfsd ùmlk"
}
```

Now you can edit your main.vsl code and add the check_spf function.

```javascript
// main.vsl
import "/addons/std/api" as api;

mail: [
  // ...
  
  rule "check_spf" || api::check_spf(ctx);

]
```

All the predefined function are under the namespace `api`. You can access to all predefined object and function using it. The `api` namespace is defined in the `addons/std/api.vsl` file.

```javascript
// api.vsl
import "/addons/std/code"
import "/addons/std/auth"
...
```

Let's add a no-relay rule for authenticated users with an embedded logging.

Create a directory `/etc/vsmtp/rules/addons/my-addons`.
Then edit a new file `my_api.vsl`.

```javascript
// my_api.vsl
//
import "../addons/std/api" as api;

//
// no-relay-mail
// 
// Behavior : if a message has a mail_from with "my_domain".
//            it must come from the local_network or the client must be authenticated.
//
// Return : accept or deny(code 550-7.1) + log
fn no_relay_mail(ctx) {
   if (ctx.mail_domain in my_domain) && ((ctx.client_ip in local_network) || (ctx.client.auth))
    { 
        vsl::accept() }
    else { 
        vsl::log(warn, "Here is my message");
        vsl::deny(api::code550_7_1) 
    }
}
```

Now you can add your rule to the main.vsl file.

```javascript
// main.vsl
import "/addons/std/api" as api;
import "/addons/my-addons/my-api" as my-api;

mail: [
    rule "check_relay" || my-api::no_relay_mail(ctx);
    rule "check_spf" || api::check_spf(ctx);
]
// ... do stuff
```
