# global::transport

Functions to configure delivery methods of emails.



<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> deliver </h2>

```rust,ignore
fn deliver(rcpt: String) -> ()
fn deliver(rcpt: SharedObject) -> ()
```

<details>
<summary markdown="span"> details </summary>

Set the delivery method to deliver for a single recipient.
After all rules are evaluated, the email will be sent
to the recipient using the domain of its address.

# Args

* `rcpt` - the recipient to apply the method to.

# Effective smtp stage

All of them.

# Examples
```ignore
#{
    delivery: [
       action "setup delivery" || transport::deliver("john.doe@example.com"),
    ]
}
```

```
# let states = vsmtp_test::vsl::run(
# |builder| Ok(builder.add_root_filter_rules(r#"
#{
  rcpt: [
    action "deliver (str/str)" || {
      envelop::add_rcpt("my.address@foo.com");
      transport::deliver("my.address@foo.com");
    },
    action "deliver (obj/str)" || {
      let rcpt = address("my.address@bar.com");
      envelop::add_rcpt(rcpt);
      transport::deliver(rcpt);
    },
    action "deliver (str/obj)" || {
      let target = ip6("::1");
      envelop::add_rcpt("my.address@baz.com");
      transport::deliver("my.address@baz.com");
    },
    action "deliver (obj/obj)" || {
      let rcpt = address("my.address@boz.com");
      envelop::add_rcpt(rcpt);
      transport::deliver(rcpt);
    },
  ],
}
# "#)?.build()));

# use vsmtp_common::{
#   transfer::{ForwardTarget, Transfer, EmailTransferStatus},
#   rcpt::Rcpt,
#   Address,
# };
# for (rcpt, addr) in states[&vsmtp_rule_engine::ExecutionStage::RcptTo].0.forward_paths().unwrap().iter().zip([
#     "my.address@foo.com",
#     "my.address@bar.com",
#     "my.address@baz.com",
#     "my.address@boz.com"
# ]) {
#   assert_eq!(
#     rcpt.address,
#     Address::new_unchecked(addr.to_string())
#   );
#   assert_eq!(
#     rcpt.transfer_method,
#     Transfer::Deliver
#   );
# }
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> deliver_all </h2>

```rust,ignore
fn deliver_all() -> ()
```

<details>
<summary markdown="span"> details </summary>

Set the delivery method to deliver for all recipients.
After all rules are evaluated, the email will be sent
to all recipients using the domain of their respective address.

# Effective smtp stage

All of them.

# Examples

```ignore
#{
    delivery: [
       action "setup delivery" || transport::deliver_all(),
    ]
}
```

```
# let states = vsmtp_test::vsl::run(
# |builder| Ok(builder.add_root_filter_rules(r#"
#{
  rcpt: [
    action "deliver_all" || {
      envelop::add_rcpt("my.address@foo.com");
      envelop::add_rcpt("my.address@bar.com");
      transport::deliver_all();
    },
  ],
}
# "#)?.build()));

# use vsmtp_common::{
#   transfer::{ForwardTarget, Transfer, EmailTransferStatus},
#   rcpt::Rcpt,
#   Address,
# };
# for (rcpt, addr) in states[&vsmtp_rule_engine::ExecutionStage::RcptTo].0.forward_paths().unwrap().iter().zip([
#     "my.address@foo.com",
#     "my.address@bar.com",
# ]) {
#   assert_eq!(
#     rcpt.address,
#     Address::new_unchecked(addr.to_string())
#   );
#   assert_eq!(
#     rcpt.transfer_method,
#     Transfer::Deliver
#   );
# }
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> forward </h2>

```rust,ignore
fn forward(rcpt: String, forward: SharedObject) -> ()
fn forward(rcpt: SharedObject, forward: String) -> ()
fn forward(rcpt: SharedObject, forward: SharedObject) -> ()
fn forward(rcpt: String, forward: String) -> ()
```

<details>
<summary markdown="span"> details </summary>

Set the delivery method to forwarding for a single recipient.
After all rules are evaluated, forwarding will be used to deliver
the email to the recipient.

# Args

* `rcpt` - the recipient to apply the method to.
* `target` - the target to forward the email to.

# Effective smtp stage

All of them.

# Examples
```ignore
#{
    delivery: [
       action "setup forwarding" || transport::forward("john.doe@example.com", "mta-john.example.com"),
    ]
}
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> forward_all </h2>

```rust,ignore
fn forward_all(forward: SharedObject) -> ()
fn forward_all(forward: String) -> ()
```

<details>
<summary markdown="span"> details </summary>

Set the delivery method to forwarding for all recipients.
After all rules are evaluated, forwarding will be used to deliver
the email.

# Args

* `target` - the target to forward the email to.

# Effective smtp stage

All of them.

# Examples

```ignore
#{
    delivery: [
       action "setup forwarding" || transport::forward_all(fqdn("mta-john.example.com")),
    ]
}
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> maildir </h2>

```rust,ignore
fn maildir(rcpt: SharedObject) -> ()
fn maildir(rcpt: String) -> ()
```

<details>
<summary markdown="span"> details </summary>

Set the delivery method to maildir for a recipient.
After all rules are evaluated, the email will be stored
locally in the `~/Maildir/new/` folder of the recipient's user if it exists on the server.

# Args

* `rcpt` - the recipient to apply the method to.

# Effective smtp stage

All of them.

# Example
```ignore
#{
    delivery: [
       action "setup maildir" || transport::maildir(address("john.doe@example.com")),
    ]
}
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> maildir_all </h2>

```rust,ignore
fn maildir_all() -> ()
```

<details>
<summary markdown="span"> details </summary>

Set the delivery method to maildir for all recipients.
After all rules are evaluated, the email will be stored
locally in each `~/Maildir/new` folder of they respective recipient
if they exists on the server.

# Effective smtp stage

All of them.

# Examples

```ignore
#{
    delivery: [
       action "setup maildir" || transport::maildir_all(),
    ]
}
```

```
# let states = vsmtp_test::vsl::run(
# |builder| Ok(builder.add_root_filter_rules(r#"
#{
  rcpt: [
    action "setup maildir" || {
        const doe = address("doe@example.com");
        envelop::add_rcpt(doe);
        envelop::add_rcpt("a@example.com");
        transport::maildir_all();
    },
  ],
}
# "#)?.build()));

# use vsmtp_common::{
#   transfer::{Transfer},
#   rcpt::Rcpt,
#   Address,
# };
# for (rcpt, addr) in states[&vsmtp_rule_engine::ExecutionStage::RcptTo].0.forward_paths().unwrap().iter().zip([
#     "doe@example.com",
#     "a@example.com",
# ]) {
#   assert_eq!(
#     rcpt.address,
#     Address::new_unchecked(addr.to_string())
#   );
#   assert_eq!(
#     rcpt.transfer_method,
#     Transfer::Maildir
#   );
# }
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> mbox </h2>

```rust,ignore
fn mbox(rcpt: String) -> ()
fn mbox(rcpt: SharedObject) -> ()
```

<details>
<summary markdown="span"> details </summary>

Set the delivery method to mbox for a recipient.
After all rules are evaluated, the email will be stored
locally in the mail box of the recipient if it exists on the server.

# Args

* `rcpt` - the recipient to apply the method to.

# Effective smtp stage

All of them.

# Examples

```ignore
#{
    delivery: [
       action "setup mbox" || transport::mbox("john.doe@example.com"),
    ]
}
```

```
# let states = vsmtp_test::vsl::run(
# |builder| Ok(builder.add_root_filter_rules(r#"
#{
  rcpt: [
    action "setup mbox" || {
        const doe = address("doe@example.com");
        envelop::add_rcpt(doe);
        envelop::add_rcpt("a@example.com");
        transport::mbox(doe);
        transport::mbox("a@example.com");
    },
  ],
}
# "#)?.build()));

# use vsmtp_common::{
#   transfer::{Transfer},
#   rcpt::Rcpt,
#   Address,
# };
# for (rcpt, addr) in states[&vsmtp_rule_engine::ExecutionStage::RcptTo].0.forward_paths().unwrap().iter().zip([
#     "doe@example.com",
#     "a@example.com",
# ]) {
#   assert_eq!(
#     rcpt.address,
#     Address::new_unchecked(addr.to_string())
#   );
#   assert_eq!(
#     rcpt.transfer_method,
#     Transfer::Mbox
#   );
# }
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> mbox_all </h2>

```rust,ignore
fn mbox_all() -> ()
```

<details>
<summary markdown="span"> details </summary>

Set the delivery method to mbox for all recipients.
After all rules are evaluated, the email will be stored
locally in the mail box of all recipients if they exists on the server.

# Effective smtp stage

All of them.

# Examples

```ignore
#{
    delivery: [
       action "setup mbox" || transport::mbox_all(),
    ]
}
```

```
# let states = vsmtp_test::vsl::run(
# |builder| Ok(builder.add_root_filter_rules(r#"
#{
  rcpt: [
    action "setup mbox" || {
        const doe = address("doe@example.com");
        envelop::add_rcpt(doe);
        envelop::add_rcpt("a@example.com");
        transport::mbox_all();
    },
  ],
}
# "#)?.build()));

# use vsmtp_common::{
#   transfer::{Transfer},
#   rcpt::Rcpt,
#   Address,
# };
# for (rcpt, addr) in states[&vsmtp_rule_engine::ExecutionStage::RcptTo].0.forward_paths().unwrap().iter().zip([
#     "doe@example.com",
#     "a@example.com",
# ]) {
#   assert_eq!(
#     rcpt.address,
#     Address::new_unchecked(addr.to_string())
#   );
#   assert_eq!(
#     rcpt.transfer_method,
#     Transfer::Mbox
#   );
# }
```
</details>

</div>
</br>

