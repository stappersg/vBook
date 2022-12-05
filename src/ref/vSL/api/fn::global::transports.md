# global::transports



<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

```rust
fn deliver(context: Context, rcpt: String) -> ()
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

```rust
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

# Example
```
#{
    delivery: [
       action "setup delivery" || deliver(address("john.doe@example.com")),
    ]
}
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

```rust
fn deliver_all(context: Context) -> ()
```

<details>
<summary markdown="span"> details </summary>

Set the delivery method to deliver for all recipients.
After all rules are evaluated, the email will be sent
to all recipients using the domain of their respective address.

# Effective smtp stage

All of them.

# Examples

```
#{
    delivery: [
       action "setup delivery" || deliver_all(),
    ]
}
```

```
 #{
   rcpt: [
     action "deliver_all" || {
       add_rcpt_envelop("my.address@foo.com");
       add_rcpt_envelop("my.address@bar.com");
       deliver_all();
     },
   ],
 }

```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

```rust
fn forward(context: Context, rcpt: SharedObject, forward: String) -> ()
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

```rust
fn forward(context: Context, rcpt: SharedObject, forward: SharedObject) -> ()
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

```rust
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
const rules = #{
    delivery: [
       action "setup forwarding" || forward("john.doe@example.com", "mta-john.example.com"),
    ]
}
```

```
#{
    rcpt: [
      action "forward (str/str)" || {
        add_rcpt_envelop("my.address@foo.com");
        forward("my.address@foo.com", "127.0.0.1");
      },
      action "forward (obj/str)" || {
        let rcpt = address("my.address@bar.com");
        add_rcpt_envelop(rcpt);
        forward(rcpt, "127.0.0.2");
      },
      action "forward (str/obj)" || {
        let target = ip6("::1");
        add_rcpt_envelop("my.address@baz.com");
        forward("my.address@baz.com", target);
      },
      action "forward (obj/obj)" || {
        let rcpt = address("my.address@boz.com");
        add_rcpt_envelop(rcpt);
        forward(rcpt, ip4("127.0.0.4"));
      },
    ],
}

```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

```rust
fn forward(context: Context, rcpt: String, forward: SharedObject) -> ()
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

```rust
fn forward_all(context: Context, forward: SharedObject) -> ()
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
       action "setup forwarding" || forward_all(fqdn("mta-john.example.com")),
    ]
}
```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

```rust
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

```rust
fn maildir(context: Context, rcpt: String) -> ()
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

# Examples
```
#{
    delivery: [
       action "setup maildir" || maildir("john.doe@example.com"),
    ]
}
```

```
 #{
   rcpt: [
     action "setup maildir" || {
         const doe = address("doe@example.com");
         add_rcpt_envelop(doe);
         add_rcpt_envelop("a@example.com");
         maildir(doe);
         maildir("a@example.com");
     },
   ],
 }

```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

```rust
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

```rust
fn maildir_all(context: Context) -> ()
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

```
#{
    delivery: [
       action "setup mbox" || mbox_all(),
    ]
}
```

```
#{
  rcpt: [
    action "setup maildir" || {
        const doe = address("doe@example.com");
        add_rcpt_envelop(doe);
        add_rcpt_envelop("a@example.com");
        maildir_all();
    },
  ],
}

```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

```rust
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

# Examples

```
#{
    delivery: [
       action "setup mbox" || mbox("john.doe@example.com"),
    ]
}
```

```
 #{
   rcpt: [
     action "setup mbox" || {
         const doe = address("doe@example.com");
         add_rcpt_envelop(doe);
         add_rcpt_envelop("a@example.com");
         mbox(doe);
         mbox("a@example.com");
     },
   ],
 }

```
</details>

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

```rust
fn mbox(context: Context, rcpt: SharedObject) -> ()
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


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

```rust
fn mbox_all(context: Context) -> ()
```

<details>
<summary markdown="span"> details </summary>

Set the delivery method to mbox for all recipients.
After all rules are evaluated, the email will be stored
locally in the mail box of all recipients if they exists on the server.

# Effective smtp stage

All of them.

# Examples

```
#{
    delivery: [
       action "setup mbox" || mbox_all(),
    ]
}
```

```
 #{
   rcpt: [
     action "setup mbox" || {
         const doe = address("doe@example.com");
         add_rcpt_envelop(doe);
         add_rcpt_envelop("a@example.com");
         mbox_all();
     },
   ],
 }

```
</details>

</div>
</br>

