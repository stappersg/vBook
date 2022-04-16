# Hardening vSMTP

First let's add a basic filtering rules.

```c
mail: [
  
  // Reject messages from internal LAN if not sent by a known user.
  rule "from_malware" || 
     if (ctx.client_ip in doe::internal_net) && !(ctx.mail in doe::family_addr) 
      { vsl::deny() } else { vsl::next() }

]
```

## Using SPF protocol (v0.11 feature)

To allow other MTAs to verify that outgoing email from Doe's family domain comes from its server, we need to enable the SPF protocol.
This is done by adding a new DNS text record that only allows only the MX record to send a mail for doe-family.com.

```shell
doe-family.com.          TXT "v=spf1 +mx -all"
```

That's all.

What about incoming messages ? vSL comes with many predefined function allowing the user to use them directly or to adapt them to his needs.
Let's browse the API folder... yes ! in rules/vls/api/eam.vsl there's a function called : check_spf().

Here is the check_spf code:

```javascript
fn check_spf(ctx) {

   
  let query_result = vsl::check_spf(ctx.client_ip, ctx.mail_from, ctx.helo);
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
  //    Issue    
  //    * trace : a trace of processing events. 
  //        <string> <== Struct viaspf::trace::Trace
  //
  // - args : client ip, sender address and optional helo/ehlo string. 
  //
  // - comments : HELO check is only performed when the HELO string is a valid domain name.

  print(query_result.spf_result)

  // Deny unwanted messages
  switch spf_result {    
    "fail" => return vsl::deny(code::550-7.23),
    "temperror" => return vsl::deny(api::code451_7_24),
    "permerror" => return vsl::deny(api::code550_7_24),  
    _ => vsl::set_header(ctx, "SPAM:" + get_header(ctx, "Subject")), 
  }

  // The message is accepted by SPF policy. 
  // Record the result in a header. 
  switch toml::server.eam.spf_header {
      "legacy" => { 
        // TO DO: identity= mailfrom/helo
        // TO DO: receiver=myname@example.com 
        value = spf_result + "\nreceiver=" + ???? hostname
                           + "client-ip="+ctx.client_ip
                           + "\nhelo="+ctx.helo
                           + 

        add_header(ctx, "Received-SPF", value)
      }
      "authentication" => 
      "both" => { 
                add_header("Received-SPF:" + result + ctx.client_ip..... + "blahbalh");
                add_header("Auth-method: SPF:" + result + ctx.client_ip..... + "blahbalh")
      
      }
      _ => throw `From SPF Check : TOML field ${toml::server.eam.spf_header} unknown`,
  }

  return 

}
```

Wait... there are two functions check_spf ? Yes.

The predefined function `api::check_spf()` calls an internal vSL function `vsl::check_spf()`.
That means that you can either utilize the predefined function `api::check_spf()` or modify/create a new one that calls `vsl::check_spf()`.

Sorry but I've got an other question: what is `toml::server.eam.spf_header` ?

That's the second big improvement of vSL. You can access to the whole configuration.

To make it works you have to add in the vsmtp.toml file the table:

```toml
[server]
# hostname = "mta-01.example.com" // default = `hostname --fqdn`

[server.eam]
spf_header = spf | authentication | both | none2
```



fn rw_subject (

  let value = get("subject");
  set("subject", SPAM + value);
)

fn check_RFC5322_compliancy {
  if has_header("from") || has_header("Date") { vsl::next() } else { vsl::deny(mycode) }
}


/// ./api-std/code.vsl
object code mycode1 {
  number: 451
  enhanced: 4.4.2
  message: "mlkfmùlkjdfsùmsfdkj ùmfdlk  fdùmkfsd ùmlk"
}

/// api.vsl
import "/api-std/code"
import "/api-std/toto"



/// main.vsl
import "/api-std/code" as code

code::mon_objet


}

object code 550 = 
```

```toml
[server.spf]
header = legacy | authentication | both | none
check_helo = true | false
```

```c
fn no-relay-mail()
   if (ctx.mail_domain in my_domain) && ((ctx.client_ip in local_network) || (ctx.client.auth))
          { vsl::accept() }
        else
          { message + vsl::deny() }
```

#{ 
  //....
  
  mail: [
    rule "no_relay_mailfrom" || no-relay-mail(ctx)
     
    rule "check_spf" || if !(ctx.client_ip in ip_whitelist) { check_spf(ctx) } else { vsl::next() }
    rule "rcpt_default" || vsl::accept(),
  ],

}
```



## Hardening outgoing messages

To allow other MTAs to verify that incoming email from Doe's family domain comes from its server, we turn on the SPF protocol.

This is done by adding a new DNS text record allowing only the MX record to send a mail for doe-family.com.

```shell
doe-family.com.          TXT "v=spf1 +mx -all"
```

### Adding an antivirus

John is aware of security issues. Malware remains a scourge on the internet.
So he decided to add a second layer of antivirus, directly on the vSMTP MTA.

He therefore installs ClamAV which comes with an online shell command, easily callable from vSMTP.

___vsmtp.toml___

```toml
... //config 

[rules]
dir = "/etc/vsmtp/rules"

[[rules.services]]
name = "antivirus"
type = "shell"
timeout = "15s"
command = "./service/clamscan.sh"
args = "{mail}"

//
// quarantine_folder is missing
//

... //config 
```

Since there is no heavy network traffic, John decided to do a pre-queue filtering.
Spool emails are quarantine in the virus_q folder.

___main.vsl___

```c
fn has_virus(services, ctx) {
    let result = services.run("antivirus", ctx);
    if result.has_signal {
        // timed out
        return false;
    }
    result.has_code && result.code != 0
}

#{
  preq: [
    rule "clam_av" || if has_virus(services, ctx) { vsl::quarantine(virus_q) } else { vsl::accept() } 
  ]
}
```

___clamscan.sh___

```bash
#!/bin/bash
echo $1 | clamscan -
exit $?
```
