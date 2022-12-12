# global::spf



<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> check_spf </h2>

```rust,ignore
fn check_spf(ctx: Context, srv: Server) -> Map

```

<details>
<summary markdown="span"> details </summary>

evaluate a sender identity.
the identity parameter can be 'helo', 'mail_from' or 'both'.

# Results
a rhai Map with:
   * result (String) : the result of an SPF evaluation.
   * cause  (String) : the "mechanism" that matched or the "problem" error (RFC 7208-9.1).
</details>

</div>
</br>

