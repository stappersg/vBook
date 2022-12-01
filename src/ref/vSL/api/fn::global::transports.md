# global::transports



<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn deliver(context: Context, rcpt: String) -> ()
```

<details>
<summary markdown="span"> details </summary>

Set the delivery method to [`Transfer::Deliver`] for a single recipient.

# Examples

```
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


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn deliver(context: Context, rcpt: SharedObject) -> ()
```

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn deliver_all(context: Context) -> ()
```

<details>
<summary markdown="span"> details </summary>

Set the delivery method to [`Transfer::Deliver`] for all recipients.

# Examples

```
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


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn forward(context: Context, rcpt: SharedObject, forward: String) -> ()
```

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn forward(context: Context, rcpt: SharedObject, forward: SharedObject) -> ()
```

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn forward(context: Context, rcpt: String, forward: String) -> ()
```

<details>
<summary markdown="span"> details </summary>

Set the delivery method to [`Transfer::Forward`] for a single recipient.

# Examples

```
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


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn forward(context: Context, rcpt: String, forward: SharedObject) -> ()
```

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn forward_all(context: Context, forward: SharedObject) -> ()
```

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn forward_all(context: Context, forward: String) -> ()
```

<details>
<summary markdown="span"> details </summary>

Set the delivery method to [`Transfer::Forward`] for all recipients.

# Examples

```
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


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn maildir(context: Context, rcpt: String) -> ()
```

<details>
<summary markdown="span"> details </summary>

Set the delivery method to [`Transfer::Maildir`] for a single recipient.

# Examples

```
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


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn maildir(context: Context, rcpt: SharedObject) -> ()
```

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn maildir_all(context: Context) -> ()
```

<details>
<summary markdown="span"> details </summary>

Set the delivery method to [`Transfer::Maildir`] for all recipients.

# Examples

```
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


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn mbox(context: Context, rcpt: SharedObject) -> ()
```

</div>
</br>


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn mbox(context: Context, rcpt: String) -> ()
```

<details>
<summary markdown="span"> details </summary>

Set the delivery method to [`Transfer::Mbox`] for a single recipient.

# Examples

```
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


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 5px; border-radius: 5px;'>

```rust
fn mbox_all(context: Context) -> ()
```

<details>
<summary markdown="span"> details </summary>

Set the delivery method to [`Transfer::Mbox`] for all recipients.

# Examples

```
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

