# global::dkim

Generate and verify DKIM signatures.
Implementation of RFC 6376. (<https://www.rfc-editor.org/rfc/rfc6376.html>)


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>get</code> auid </h2>

```rust,ignore
fn get auid(signature: Signature) -> String
```

<details>
<summary markdown="span"> details </summary>

return the `auid` property of the [`Signature`]
</details>

</div>
</br>

<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>get</code> sdid </h2>

```rust,ignore
fn get sdid(signature: Signature) -> String
```

<details>
<summary markdown="span"> details </summary>

return the `sdid` property of the [`Signature`]
</details>

</div>
</br>

<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> get_private_keys </h2>

```rust,ignore
fn get_private_keys(sdid: String) -> Array
```

<details>
<summary markdown="span"> details </summary>

Get the list of DKIM private keys associated with this sdid
</details>

</div>
</br>

<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> has_result </h2>

```rust,ignore
fn has_result() -> bool
```

<details>
<summary markdown="span"> details </summary>

Has the `ctx()` a DKIM signature verification result ?
</details>

</div>
</br>

<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> result </h2>

```rust,ignore
fn result() -> Map
```

<details>
<summary markdown="span"> details </summary>

Return the DKIM signature verification result in the `ctx()` or
an error if no result is found.
</details>

</div>
</br>

<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> sign </h2>

```rust,ignore
fn sign(params: Map) -> ()
```

<details>
<summary markdown="span"> details </summary>

Produce a `DKIM-Signature` header.

# Args

* `selector` - the DNS selector to expose the public key & for the verifier
* `private_key` - the private key to sign the mail,
    associated with the public key in the `selector._domainkey.sdid` DNS record
* `headers_field` - list of headers to sign
* `canonicalization` - the canonicalization algorithm to use (ex: "simple/relaxed")

# Effective smtp stage

`preq` and onwards.

# Example

```text
#{
  preq: [
    action "sign dkim" || {
      for private_key in dkim::get_private_keys("testserver.com") {
        dkim::sign(#{
           // default: server_name()
           sdid:                "testserver.com",

           // mandatory
           selector:            "2022-09",

           // mandatory
           private_key:         private_key,

           // default: ["From", "To", "Date", "Subject", "From"]
           headers:             ["From", "To", "Date", "Subject", "From"],

           // default: "simple/relaxed"
           canonicalization:    "simple/relaxed"
        });
      }
    }
  ]
}
```
</details>

</div>
</br>

<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> store </h2>

```rust,ignore
fn store(result: Map) -> ()
```

<details>
<summary markdown="span"> details </summary>

Store the result produced by the DKIM signature verification in the `ctx()`.

# Error
* The `status` field is missing in the DKIM verification results.
</details>

</div>
</br>

<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> verify </h2>

```rust,ignore
fn verify() -> Map
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

#{
    preq: [
        rule "verify dkim" || {
            dkim::verify();

            // The dkim header should indicate a pass.
            if !msg::get_header("Authentication-Results").contains("dkim=pass") {
              return state::deny();
            }

            // the result of dkim verification is cached, so this call will
            // not recompute the signature and recreate a header.
            dkim::verify();

            // FIXME: should be one.
            if msg::count_header("Authentication-Results") != 2 {
              return state::deny();
            }

            state::accept()
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

let rules = r#"#{
    preq: [
        rule "verify dkim" || {
            dkim::verify();

            if !msg::get_header("Authentication-Results").contains("dkim=fail") {
              return state::deny();
            }

            state::accept();
        }
    ]
}"#;

```
</details>

</div>
</br>
