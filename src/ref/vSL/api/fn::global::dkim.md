# global::dkim



<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> generate_signature_dkim </h2>

```rust,ignore
fn generate_signature_dkim(message: Message, context: Context, selector: String, private_key: Arc<PrivateKey>, headers_field: Array, canonicalization: String) -> String

```

<details>
<summary markdown="span"> details </summary>

Create a new signature of the message for the DKIM.

# Examples

```
let msg = r#"
Date: Wed, 26 Oct 2022 14:30:51 -0700
From: Mathieu Lala <noreply@github.com>
To: mlala@negabit.com
Subject: Testing and documenting the dkim signature

This message has not been signed yet, meaning someone could change it...
"#;



 #{
   postq: [
     action "add a DKIM signature" || {
       for i in get_private_keys(srv(), "testserver.com") {
         sign_dkim("2022-09", i, ["From", "To", "Date", "Subject", "From"], "simple/relaxed");
       }
     },
     rule "check signature" || {
       let signature = "v=1; a=rsa-sha256; d=testserver.com; s=2022-09;\r\n\
           \tc=simple/relaxed; q=dns/txt; h=From:To:Date:Subject:From;\r\n\
           \tbh=ATHiC1KD8OegIorswWts+SlujGUpgqR6pqXYlNWA01Y=;\r\n\tb=Ur\
           /frdH3beyU3LRQMGBdI6OdxRvfpu+s04hmHcVkpBYzR4cXuDPByWpUCqhO4C\
           sEwpPRDcWQtsCfuzSK1FTf7XCWgsKKGPmsdQ40pUviA0UrrzpIDIziMxSI/S\
           8ohNnxvqxrtxZoN6Wo2lnQ+kYAATYxJPOjC57JIBJ89RGrf+6Wbvz6/PofcU\
           9VwpylegZRU5Cial69lN2qaIkoVFOE9fz8ZIz9VV2A9Lh/xgKFM7eipBWCR6\
           ZUU1HZTbSiqiL9Q6A823az/E2jqOUZXtsGK/Bo/vDjTV166d5vY34JA3189C\
           x83Rbif9A/kdCO6C8gGK0WOasp5R0ONmVz41TaGQ==";

       if get_header("DKIM-Signature") == signature {
         accept()
       } else {
         deny()
       }
     }
   ]
 }

```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> dkim_result </h2>

```rust,ignore
fn get dkim_result(ctx: Context) -> Map

```

<details>
<summary markdown="span"> details </summary>

Return the DKIM signature verification result in the `ctx()` or
an error if no result is found.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> has_dkim_result </h2>

```rust,ignore
fn get has_dkim_result(ctx: Context) -> bool

```

<details>
<summary markdown="span"> details </summary>

Has the `ctx()` a DKIM signature verification result ?
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> get_private_keys </h2>

```rust,ignore
fn get_private_keys(server: Server, sdid: String) -> Array

```

<details>
<summary markdown="span"> details </summary>

Get the list of DKIM private keys associated with this sdid
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> handle_dkim_error </h2>

```rust,ignore
fn handle_dkim_error(err: ?) -> String

```

<details>
<summary markdown="span"> details </summary>

get the dkim status from an error produced by this module

# Error
* The given parameter is not a Map.
* `type` field not found in parameter / is not a string.
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> parse_signature </h2>

```rust,ignore
fn parse_signature(input: String) -> Signature

```

<details>
<summary markdown="span"> details </summary>

create a [`Signature`] from a `DKIM-Signature` header
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> verify_dkim </h2>

```rust,ignore
fn verify_dkim(message: Message, signature: Signature, key: PublicKey) -> ()

```

<details>
<summary markdown="span"> details </summary>

Operate the hashing of the `message`'s headers and body, and compare the result with the
`signature` and `key` data.

# Examples

```
// The message received.
let msg = r#"
Received: from github.com (hubbernetes-node-54a15d2.ash1-iad.github.net [10.56.202.84])
	by smtp.github.com (Postfix) with ESMTPA id 19FB45E0B6B
	for <mlala@negabit.com>; Wed, 26 Oct 2022 14:30:51 -0700 (PDT)
DKIM-Signature: v=1; a=rsa-sha256; c=relaxed/relaxed; d=github.com;
	s=pf2014; t=1666819851;
	bh=7gTTczemS/Aahap1SpEnunm4pAPNuUIg7fUzwEx0QUA=;
	h=Date:From:To:Subject:From;
	b=eAufMk7uj4R+bO5Nr4DymffdGdbrJNza1+eykatgZED6tBBcMidkMiLSnP8FyVCS9
	 /GSlXME6/YffAXg4JEBr2lN3PuLIf94S86U3VckuoQQQe1LPtHlnGW5ZwJgi6DjrzT
	 klht/6Pn1w3a2jdNSDccWhk5qlSOQX9JKnE7UD58=
Date: Wed, 26 Oct 2022 14:30:51 -0700
From: Mathieu Lala <noreply@github.com>
To: mlala@negabit.com
Message-ID: <viridIT/vSMTP/push/refs/heads/test/rule-engine/000000-c6459a@github.com>
Subject: [viridIT/vSMTP] c6459a: test: add test on message
Mime-Version: 1.0
Content-Type: text/plain;
 charset=UTF-8
Content-Transfer-Encoding: 7bit
Approved: =?UTF-8?Q?hello_there_=F0=9F=91=8B?=
X-GitHub-Recipient-Address: mlala@negabit.com
X-Auto-Response-Suppress: All

  Branch: refs/heads/test/rule-engine
  Home:   https://github.com/viridIT/vSMTP
  Commit: c6459a4946395ba90182ce7181bdbc327994c038
      https://github.com/viridIT/vSMTP/commit/c6459a4946395ba90182ce7181bdbc327994c038
  Author: Mathieu Lala <m.lala@viridit.com>
  Date:   2022-10-26 (Wed, 26 Oct 2022)

  Changed paths:
    M src/vsmtp/vsmtp-rule-engine/src/api/message.rs
    M src/vsmtp/vsmtp-rule-engine/src/lib.rs
    M src/vsmtp/vsmtp-test/src/vsl.rs

  Log Message:
  -----------
  test: add test on message


"#;

 // Rules
 #{
   preq: [
     rule "verify_dkim" || {
       verify_dkim();
       if !get_header("Authentication-Results").contains("dkim=pass") {
         return deny();
       }
       // the result of dkim verification is cached, so this call will
       // not recompute the signature and recreate a header
       verify_dkim();

       // FIXME: should be one
       if count_header("Authentication-Results") != 2 {
         return deny();
       }

       accept();
     }
   ]
 }
```

Changing the header `Subject` will result in a dkim verification failure.

```
// The message received.
let msg = r#"
Received: from github.com (hubbernetes-node-54a15d2.ash1-iad.github.net [10.56.202.84])
	by smtp.github.com (Postfix) with ESMTPA id 19FB45E0B6B
	for <mlala@negabit.com>; Wed, 26 Oct 2022 14:30:51 -0700 (PDT)
DKIM-Signature: v=1; a=rsa-sha256; c=relaxed/relaxed; d=github.com;
	s=pf2014; t=1666819851;
	bh=7gTTczemS/Aahap1SpEnunm4pAPNuUIg7fUzwEx0QUA=;
	h=Date:From:To:Subject:From;
	b=eAufMk7uj4R+bO5Nr4DymffdGdbrJNza1+eykatgZED6tBBcMidkMiLSnP8FyVCS9
	 /GSlXME6/YffAXg4JEBr2lN3PuLIf94S86U3VckuoQQQe1LPtHlnGW5ZwJgi6DjrzT
	 klht/6Pn1w3a2jdNSDccWhk5qlSOQX9JKnE7UD58=
Date: Wed, 26 Oct 2022 14:30:51 -0700
From: Mathieu Lala <noreply@github.com>
To: mlala@negabit.com
Message-ID: <viridIT/vSMTP/push/refs/heads/test/rule-engine/000000-c6459a@github.com>
Subject: Changing the header produce an invalid dkim verification
Mime-Version: 1.0
Content-Type: text/plain;
 charset=UTF-8
Content-Transfer-Encoding: 7bit
Approved: =?UTF-8?Q?hello_there_=F0=9F=91=8B?=
X-GitHub-Recipient-Address: mlala@negabit.com
X-Auto-Response-Suppress: All

  Branch: refs/heads/test/rule-engine
  Home:   https://github.com/viridIT/vSMTP
  Commit: c6459a4946395ba90182ce7181bdbc327994c038
      https://github.com/viridIT/vSMTP/commit/c6459a4946395ba90182ce7181bdbc327994c038
  Author: Mathieu Lala <m.lala@viridit.com>
  Date:   2022-10-26 (Wed, 26 Oct 2022)

  Changed paths:
    M src/vsmtp/vsmtp-rule-engine/src/api/message.rs
    M src/vsmtp/vsmtp-rule-engine/src/lib.rs
    M src/vsmtp/vsmtp-test/src/vsl.rs

  Log Message:
  -----------
  test: add test on message
"#;

let rules = r"#{
    preq: [
      rule "verify_dkim" || {
        verify_dkim();
        if !get_header("Authentication-Results").contains("dkim=fail") {
          return deny();
        }
        accept();
      }
    ]
}"#;

```
</details>

</div>
</br>

