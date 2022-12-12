# global::transports



<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> deliver </h2>

```rust,ignore
fn deliver(context: Context, rcpt: String) -> ()
fn deliver(context: Context, rcpt: SharedObject) -> ()
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
```
#{
    delivery: [
       action "setup delivery" || deliver("john.doe@example.com"),
    ]
}
```

```
 #{
   rcpt: [
     action "deliver (str/str)" || {
       add_rcpt_envelop("my.address@foo.com");
       deliver("my.address@foo.com");
     },
     action "deliver (obj/str)" || {
       let rcpt = address("my.address@bar.com");
       add_rcpt_envelop(rcpt);
       deliver(rcpt);
     },
     action "deliver (str/obj)" || {
       let target = ip6("::1");
       add_rcpt_envelop("my.address@baz.com");
       deliver("my.address@baz.com");
     },
     action "deliver (obj/obj)" || {
       let rcpt = address("my.address@boz.com");
       add_rcpt_envelop(rcpt);
       deliver(rcpt);
     },
   ],
 }

```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> forward </h2>

```rust,ignore
fn forward(context: Context, rcpt: String, forward: SharedObject) -> ()
fn forward(context: Context, rcpt: SharedObject, forward: SharedObject) -> ()
fn forward(context: Context, rcpt: SharedObject, forward: String) -> ()
fn forward(context: Context, rcpt: String, forward: String) -> ()
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
```
#{
    delivery: [
       action "setup forwarding" || forward("john.doe@example.com", "mta-john.example.com"),
    ]
}
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> forward_all </h2>

```rust,ignore
fn forward_all(context: Context, forward: String) -> ()

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

```
#{
    delivery: [
       action "setup forwarding" || forward_all("mta-john.example.com"),
    ]
}
```

```
 #{
   rcpt: [
     action "forward_all" || {
       add_rcpt_envelop("my.address@foo.com");
       add_rcpt_envelop("my.address@bar.com");
       forward_all("127.0.0.1");
     },
     action "forward_all (obj)" || {
       add_rcpt_envelop("my.address@foo2.com");
       add_rcpt_envelop("my.address@bar2.com");
       forward_all(ip4("127.0.0.1"));
     },
   ],
 }

```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> maildir </h2>

```rust,ignore
fn maildir(context: Context, rcpt: SharedObject) -> ()

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
```
#{
    delivery: [
       action "setup maildir" || maildir(address("john.doe@example.com")),
    ]
}
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> mbox </h2>

```rust,ignore
fn mbox(context: Context, rcpt: SharedObject) -> ()
fn mbox(context: Context, rcpt: String) -> ()
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

# Example
```
#{
    delivery: [
       action "setup mbox" || mbox(address("john.doe@example.com")),
    ]
}
```
</details>

</div>
</br>

