# global::transport

Functions to configure delivery methods of emails.


<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> forward </h2>

```rust,ignore
fn forward(rcpt: SharedObject, forward: String) -> ()
fn forward(rcpt: String, forward: SharedObject) -> ()
fn forward(rcpt: SharedObject, forward: SharedObject) -> ()
fn forward(rcpt: String, forward: String) -> ()
```

<div class="tab">
    <button
    group="forward"
    id="link-forward-description"
    class="tablinks active"
    onclick="openTab(event, 'forward', 'description')">
        Description
    </button>
    <button
    group="forward"
    id="link-forward-Args"
    class="tablinks"
    onclick="openTab(event, 'forward', 'Args')">
        Args
    </button>
    <button
    group="forward"
    id="link-forward-Effective smtp stage"
    class="tablinks"
    onclick="openTab(event, 'forward', 'Effective smtp stage')">
        Effective smtp stage
    </button>
    <button
    group="forward"
    id="link-forward-Examples"
    class="tablinks"
    onclick="openTab(event, 'forward', 'Examples')">
        Examples
    </button></div>

<div group="forward" id="forward-description" style="display: block;" markdown="span" class="tabcontent">
Set the delivery method to forwarding for a single recipient.
After all rules are evaluated, forwarding will be used to deliver
the email to the recipient.


</div>

<div group="forward" id="forward-Args" class="tabcontent">

* `rcpt` - the recipient to apply the method to.
* `target` - the target to forward the email to.


</div>

<div group="forward" id="forward-Effective smtp stage" class="tabcontent">

All of them.


</div>

<div group="forward" id="forward-Examples" class="tabcontent">

```
#{
    rcpt: [
      action "forward (str/str)" || {
        envelop::add_rcpt("my.address@foo.com");
        transport::forward("my.address@foo.com", "127.0.0.1");
      },
      action "forward (obj/str)" || {
        let rcpt = address("my.address@bar.com");
        envelop::add_rcpt(rcpt);
        transport::forward(rcpt, "127.0.0.2");
      },
      action "forward (str/obj)" || {
        let target = ip6("::1");
        envelop::add_rcpt("my.address@baz.com");
        transport::forward("my.address@baz.com", target);
      },
      action "forward (obj/obj)" || {
        let rcpt = address("my.address@boz.com");
        envelop::add_rcpt(rcpt);
        transport::forward(rcpt, ip4("127.0.0.4"));
      },
    ],
}
```

Or with url:

```
#{
    rcpt: [
      action "set forward" || {
        let user = "root@domain.tld";
        let pass = "xxxxxx";
        let host = "smtp.domain.tld";
        let port = 25;
        transport::forward_all(`smtp://${user}:${pass}@${host}:${port}?tls=opportunistic`);
      },
   ]
}
```
</div>

</div>
</br>

<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> forward_all </h2>

```rust,ignore
fn forward_all(forward: SharedObject) -> ()
fn forward_all(forward: String) -> ()
```

<div class="tab">
    <button
    group="forward_all"
    id="link-forward_all-description"
    class="tablinks active"
    onclick="openTab(event, 'forward_all', 'description')">
        Description
    </button>
    <button
    group="forward_all"
    id="link-forward_all-Args"
    class="tablinks"
    onclick="openTab(event, 'forward_all', 'Args')">
        Args
    </button>
    <button
    group="forward_all"
    id="link-forward_all-Effective smtp stage"
    class="tablinks"
    onclick="openTab(event, 'forward_all', 'Effective smtp stage')">
        Effective smtp stage
    </button>
    <button
    group="forward_all"
    id="link-forward_all-Examples"
    class="tablinks"
    onclick="openTab(event, 'forward_all', 'Examples')">
        Examples
    </button></div>

<div group="forward_all" id="forward_all-description" style="display: block;" markdown="span" class="tabcontent">
Set the delivery method to forwarding for all recipients.
After all rules are evaluated, forwarding will be used to deliver
the email.


</div>

<div group="forward_all" id="forward_all-Args" class="tabcontent">

* `target` - the target to forward the email to.


</div>

<div group="forward_all" id="forward_all-Effective smtp stage" class="tabcontent">

All of them.


</div>

<div group="forward_all" id="forward_all-Examples" class="tabcontent">

```
#{
  rcpt: [
    action "forward_all" || {
      envelop::add_rcpt("my.address@foo.com");
      envelop::add_rcpt("my.address@bar.com");
      transport::forward_all("127.0.0.1");
    },
    action "forward_all (obj)" || {
      envelop::add_rcpt("my.address@foo2.com");
      envelop::add_rcpt("my.address@bar2.com");
      transport::forward_all(ip4("127.0.0.1"));
    },
  ],
}


```
</div>

</div>
</br>

<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> deliver </h2>

```rust,ignore
fn deliver(rcpt: String) -> ()
fn deliver(rcpt: SharedObject) -> ()
```

<div class="tab">
    <button
    group="deliver"
    id="link-deliver-description"
    class="tablinks active"
    onclick="openTab(event, 'deliver', 'description')">
        Description
    </button>
    <button
    group="deliver"
    id="link-deliver-Args"
    class="tablinks"
    onclick="openTab(event, 'deliver', 'Args')">
        Args
    </button>
    <button
    group="deliver"
    id="link-deliver-Effective smtp stage"
    class="tablinks"
    onclick="openTab(event, 'deliver', 'Effective smtp stage')">
        Effective smtp stage
    </button>
    <button
    group="deliver"
    id="link-deliver-Examples"
    class="tablinks"
    onclick="openTab(event, 'deliver', 'Examples')">
        Examples
    </button></div>

<div group="deliver" id="deliver-description" style="display: block;" markdown="span" class="tabcontent">
Set the delivery method to deliver for a single recipient.
After all rules are evaluated, the email will be sent
to the recipient using the domain of its address.


</div>

<div group="deliver" id="deliver-Args" class="tabcontent">

* `rcpt` - the recipient to apply the method to.


</div>

<div group="deliver" id="deliver-Effective smtp stage" class="tabcontent">

All of them.


</div>

<div group="deliver" id="deliver-Examples" class="tabcontent">

```
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


```
</div>

</div>
</br>

<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> deliver_all </h2>

```rust,ignore
fn deliver_all() -> ()
```

<div class="tab">
    <button
    group="deliver_all"
    id="link-deliver_all-description"
    class="tablinks active"
    onclick="openTab(event, 'deliver_all', 'description')">
        Description
    </button>
    <button
    group="deliver_all"
    id="link-deliver_all-Effective smtp stage"
    class="tablinks"
    onclick="openTab(event, 'deliver_all', 'Effective smtp stage')">
        Effective smtp stage
    </button>
    <button
    group="deliver_all"
    id="link-deliver_all-Examples"
    class="tablinks"
    onclick="openTab(event, 'deliver_all', 'Examples')">
        Examples
    </button>
    <button
    group="deliver_all"
    id="link-deliver_all-let rules = r#""
    class="tablinks"
    onclick="openTab(event, 'deliver_all', 'let rules = r#"')">
        let rules = r#"
    </button>
    <button
    group="deliver_all"
    id="link-deliver_all-     action "rm default value" || {"
    class="tablinks"
    onclick="openTab(event, 'deliver_all', '     action "rm default value" || {')">
             action "rm default value" || {
    </button>
    <button
    group="deliver_all"
    id="link-deliver_all-       envelop::rm_rcpt("recipient@testserver.com");"
    class="tablinks"
    onclick="openTab(event, 'deliver_all', '       envelop::rm_rcpt("recipient@testserver.com");')">
               envelop::rm_rcpt("recipient@testserver.com");
    </button>
    <button
    group="deliver_all"
    id="link-deliver_all-     },"
    class="tablinks"
    onclick="openTab(event, 'deliver_all', '     },')">
             },
    </button>
    <button
    group="deliver_all"
    id="link-deliver_all-"#;"
    class="tablinks"
    onclick="openTab(event, 'deliver_all', '"#;')">
        "#;
    </button>
    <button
    group="deliver_all"
    id="link-deliver_all-let states = vsmtp_test::vsl::run(|builder| Ok(builder"
    class="tablinks"
    onclick="openTab(event, 'deliver_all', 'let states = vsmtp_test::vsl::run(|builder| Ok(builder')">
        let states = vsmtp_test::vsl::run(|builder| Ok(builder
    </button>
    <button
    group="deliver_all"
    id="link-deliver_all-  .add_root_filter_rules("#{}")?"
    class="tablinks"
    onclick="openTab(event, 'deliver_all', '  .add_root_filter_rules("#{}")?')">
          .add_root_filter_rules("#{}")?
    </button>
    <button
    group="deliver_all"
    id="link-deliver_all-     .add_domain_rules("testserver.com".parse().unwrap())"
    class="tablinks"
    onclick="openTab(event, 'deliver_all', '     .add_domain_rules("testserver.com".parse().unwrap())')">
             .add_domain_rules("testserver.com".parse().unwrap())
    </button>
    <button
    group="deliver_all"
    id="link-deliver_all-       .with_incoming(rules)?"
    class="tablinks"
    onclick="openTab(event, 'deliver_all', '       .with_incoming(rules)?')">
               .with_incoming(rules)?
    </button>
    <button
    group="deliver_all"
    id="link-deliver_all-       .with_outgoing(rules)?"
    class="tablinks"
    onclick="openTab(event, 'deliver_all', '       .with_outgoing(rules)?')">
               .with_outgoing(rules)?
    </button>
    <button
    group="deliver_all"
    id="link-deliver_all-       .with_internal(rules)?"
    class="tablinks"
    onclick="openTab(event, 'deliver_all', '       .with_internal(rules)?')">
               .with_internal(rules)?
    </button>
    <button
    group="deliver_all"
    id="link-deliver_all-     .build()"
    class="tablinks"
    onclick="openTab(event, 'deliver_all', '     .build()')">
             .build()
    </button>
    <button
    group="deliver_all"
    id="link-deliver_all-  .build())"
    class="tablinks"
    onclick="openTab(event, 'deliver_all', '  .build())')">
          .build())
    </button>
    <button
    group="deliver_all"
    id="link-deliver_all-);"
    class="tablinks"
    onclick="openTab(event, 'deliver_all', ');')">
        );
    </button>
    <button
    group="deliver_all"
    id="link-deliver_all-assert_eq!(states[&vsmtp_rule_engine::ExecutionStage::RcptTo].2, vsmtp_common::status::Status::Next);"
    class="tablinks"
    onclick="openTab(event, 'deliver_all', 'assert_eq!(states[&vsmtp_rule_engine::ExecutionStage::RcptTo].2, vsmtp_common::status::Status::Next);')">
        assert_eq!(states[&vsmtp_rule_engine::ExecutionStage::RcptTo].2, vsmtp_common::status::Status::Next);
    </button>
    <button
    group="deliver_all"
    id="link-deliver_all-use vsmtp_common::Address;"
    class="tablinks"
    onclick="openTab(event, 'deliver_all', 'use vsmtp_common::Address;')">
        use vsmtp_common::Address;
    </button>
    <button
    group="deliver_all"
    id="link-deliver_all-let transport = std::sync::Arc::new("
    class="tablinks"
    onclick="openTab(event, 'deliver_all', 'let transport = std::sync::Arc::new(')">
        let transport = std::sync::Arc::new(
    </button>
    <button
    group="deliver_all"
    id="link-deliver_all-  vsmtp_delivery::Deliver::new("
    class="tablinks"
    onclick="openTab(event, 'deliver_all', '  vsmtp_delivery::Deliver::new(')">
          vsmtp_delivery::Deliver::new(
    </button>
    <button
    group="deliver_all"
    id="link-deliver_all-    std::sync::Arc::new(trust_dns_resolver::TokioAsyncResolver::tokio_from_system_conf().unwrap()),"
    class="tablinks"
    onclick="openTab(event, 'deliver_all', '    std::sync::Arc::new(trust_dns_resolver::TokioAsyncResolver::tokio_from_system_conf().unwrap()),')">
            std::sync::Arc::new(trust_dns_resolver::TokioAsyncResolver::tokio_from_system_conf().unwrap()),
    </button>
    <button
    group="deliver_all"
    id="link-deliver_all-    std::sync::Arc::new(vsmtp_test::config::local_test())"
    class="tablinks"
    onclick="openTab(event, 'deliver_all', '    std::sync::Arc::new(vsmtp_test::config::local_test())')">
            std::sync::Arc::new(vsmtp_test::config::local_test())
    </button>
    <button
    group="deliver_all"
    id="link-deliver_all-  )"
    class="tablinks"
    onclick="openTab(event, 'deliver_all', '  )')">
          )
    </button>
    <button
    group="deliver_all"
    id="link-deliver_all-);"
    class="tablinks"
    onclick="openTab(event, 'deliver_all', ');')">
        );
    </button>
    <button
    group="deliver_all"
    id="link-deliver_all-let bound = states[&vsmtp_rule_engine::ExecutionStage::RcptTo].0.delivery().unwrap().get("
    class="tablinks"
    onclick="openTab(event, 'deliver_all', 'let bound = states[&vsmtp_rule_engine::ExecutionStage::RcptTo].0.delivery().unwrap().get(')">
        let bound = states[&vsmtp_rule_engine::ExecutionStage::RcptTo].0.delivery().unwrap().get(
    </button>
    <button
    group="deliver_all"
    id="link-deliver_all-  &vsmtp_common::transport::WrapperSerde::Ready(transport)"
    class="tablinks"
    onclick="openTab(event, 'deliver_all', '  &vsmtp_common::transport::WrapperSerde::Ready(transport)')">
          &vsmtp_common::transport::WrapperSerde::Ready(transport)
    </button>
    <button
    group="deliver_all"
    id="link-deliver_all-).unwrap();"
    class="tablinks"
    onclick="openTab(event, 'deliver_all', ').unwrap();')">
        ).unwrap();
    </button>
    <button
    group="deliver_all"
    id="link-deliver_all-for (addr, expected_addr) in states[&vsmtp_rule_engine::ExecutionStage::RcptTo].0.forward_paths().unwrap().iter().zip(["
    class="tablinks"
    onclick="openTab(event, 'deliver_all', 'for (addr, expected_addr) in states[&vsmtp_rule_engine::ExecutionStage::RcptTo].0.forward_paths().unwrap().iter().zip([')">
        for (addr, expected_addr) in states[&vsmtp_rule_engine::ExecutionStage::RcptTo].0.forward_paths().unwrap().iter().zip([
    </button>
    <button
    group="deliver_all"
    id="link-deliver_all-    "my.address@foo.com","
    class="tablinks"
    onclick="openTab(event, 'deliver_all', '    "my.address@foo.com",')">
            "my.address@foo.com",
    </button>
    <button
    group="deliver_all"
    id="link-deliver_all-    "my.address@bar.com","
    class="tablinks"
    onclick="openTab(event, 'deliver_all', '    "my.address@bar.com",')">
            "my.address@bar.com",
    </button>
    <button
    group="deliver_all"
    id="link-deliver_all-]) {"
    class="tablinks"
    onclick="openTab(event, 'deliver_all', ']) {')">
        ]) {
    </button>
    <button
    group="deliver_all"
    id="link-deliver_all-  assert_eq!("
    class="tablinks"
    onclick="openTab(event, 'deliver_all', '  assert_eq!(')">
          assert_eq!(
    </button>
    <button
    group="deliver_all"
    id="link-deliver_all-    *addr,"
    class="tablinks"
    onclick="openTab(event, 'deliver_all', '    *addr,')">
            *addr,
    </button>
    <button
    group="deliver_all"
    id="link-deliver_all-    Address::new_unchecked(expected_addr.to_string())"
    class="tablinks"
    onclick="openTab(event, 'deliver_all', '    Address::new_unchecked(expected_addr.to_string())')">
            Address::new_unchecked(expected_addr.to_string())
    </button>
    <button
    group="deliver_all"
    id="link-deliver_all-  );"
    class="tablinks"
    onclick="openTab(event, 'deliver_all', '  );')">
          );
    </button>
    <button
    group="deliver_all"
    id="link-deliver_all-  assert!(bound.iter().map(|(r, _)| r).any(|r| *r == *addr));"
    class="tablinks"
    onclick="openTab(event, 'deliver_all', '  assert!(bound.iter().map(|(r, _)| r).any(|r| *r == *addr));')">
          assert!(bound.iter().map(|(r, _)| r).any(|r| *r == *addr));
    </button>
    <button
    group="deliver_all"
    id="link-deliver_all-}"
    class="tablinks"
    onclick="openTab(event, 'deliver_all', '}')">
        }
    </button></div>

<div group="deliver_all" id="deliver_all-description" style="display: block;" markdown="span" class="tabcontent">
Set the delivery method to deliver for all recipients.
After all rules are evaluated, the email will be sent
to all recipients using the domain of their respective address.


</div>

<div group="deliver_all" id="deliver_all-Effective smtp stage" class="tabcontent">

All of them.


</div>

<div group="deliver_all" id="deliver_all-Examples" class="tabcontent">

```ignore
#{
    delivery: [
       action "setup delivery" || transport::deliver_all(),
    ]
}
```

```

</div>

<div group="deliver_all" id="deliver_all-let rules = r#"" class="tabcontent">
#{
  rcpt: [

</div>

<div group="deliver_all" id="deliver_all-     action "rm default value" || {" class="tabcontent">

</div>

<div group="deliver_all" id="deliver_all-       envelop::rm_rcpt("recipient@testserver.com");" class="tabcontent">

</div>

<div group="deliver_all" id="deliver_all-     }," class="tabcontent">
    action "deliver_all" || {
      envelop::add_rcpt("my.address@foo.com");
      envelop::add_rcpt("my.address@bar.com");
      transport::deliver_all();
    },
  ],
}

</div>

<div group="deliver_all" id="deliver_all-"#;" class="tabcontent">


</div>

<div group="deliver_all" id="deliver_all-let states = vsmtp_test::vsl::run(|builder| Ok(builder" class="tabcontent">

</div>

<div group="deliver_all" id="deliver_all-  .add_root_filter_rules("#{}")?" class="tabcontent">

</div>

<div group="deliver_all" id="deliver_all-     .add_domain_rules("testserver.com".parse().unwrap())" class="tabcontent">

</div>

<div group="deliver_all" id="deliver_all-       .with_incoming(rules)?" class="tabcontent">

</div>

<div group="deliver_all" id="deliver_all-       .with_outgoing(rules)?" class="tabcontent">

</div>

<div group="deliver_all" id="deliver_all-       .with_internal(rules)?" class="tabcontent">

</div>

<div group="deliver_all" id="deliver_all-     .build()" class="tabcontent">

</div>

<div group="deliver_all" id="deliver_all-  .build())" class="tabcontent">

</div>

<div group="deliver_all" id="deliver_all-);" class="tabcontent">

</div>

<div group="deliver_all" id="deliver_all-assert_eq!(states[&vsmtp_rule_engine::ExecutionStage::RcptTo].2, vsmtp_common::status::Status::Next);" class="tabcontent">

</div>

<div group="deliver_all" id="deliver_all-use vsmtp_common::Address;" class="tabcontent">

</div>

<div group="deliver_all" id="deliver_all-let transport = std::sync::Arc::new(" class="tabcontent">

</div>

<div group="deliver_all" id="deliver_all-  vsmtp_delivery::Deliver::new(" class="tabcontent">

</div>

<div group="deliver_all" id="deliver_all-    std::sync::Arc::new(trust_dns_resolver::TokioAsyncResolver::tokio_from_system_conf().unwrap())," class="tabcontent">

</div>

<div group="deliver_all" id="deliver_all-    std::sync::Arc::new(vsmtp_test::config::local_test())" class="tabcontent">

</div>

<div group="deliver_all" id="deliver_all-  )" class="tabcontent">

</div>

<div group="deliver_all" id="deliver_all-);" class="tabcontent">

</div>

<div group="deliver_all" id="deliver_all-let bound = states[&vsmtp_rule_engine::ExecutionStage::RcptTo].0.delivery().unwrap().get(" class="tabcontent">

</div>

<div group="deliver_all" id="deliver_all-  &vsmtp_common::transport::WrapperSerde::Ready(transport)" class="tabcontent">

</div>

<div group="deliver_all" id="deliver_all-).unwrap();" class="tabcontent">

</div>

<div group="deliver_all" id="deliver_all-for (addr, expected_addr) in states[&vsmtp_rule_engine::ExecutionStage::RcptTo].0.forward_paths().unwrap().iter().zip([" class="tabcontent">

</div>

<div group="deliver_all" id="deliver_all-    "my.address@foo.com"," class="tabcontent">

</div>

<div group="deliver_all" id="deliver_all-    "my.address@bar.com"," class="tabcontent">

</div>

<div group="deliver_all" id="deliver_all-]) {" class="tabcontent">

</div>

<div group="deliver_all" id="deliver_all-  assert_eq!(" class="tabcontent">

</div>

<div group="deliver_all" id="deliver_all-    *addr," class="tabcontent">

</div>

<div group="deliver_all" id="deliver_all-    Address::new_unchecked(expected_addr.to_string())" class="tabcontent">

</div>

<div group="deliver_all" id="deliver_all-  );" class="tabcontent">

</div>

<div group="deliver_all" id="deliver_all-  assert!(bound.iter().map(|(r, _)| r).any(|r| *r == *addr));" class="tabcontent">

</div>

<div group="deliver_all" id="deliver_all-}" class="tabcontent">
```
</div>

</div>
</br>

<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> mbox </h2>

```rust,ignore
fn mbox(rcpt: String) -> ()
fn mbox(rcpt: SharedObject) -> ()
```

<div class="tab">
    <button
    group="mbox"
    id="link-mbox-description"
    class="tablinks active"
    onclick="openTab(event, 'mbox', 'description')">
        Description
    </button>
    <button
    group="mbox"
    id="link-mbox-Args"
    class="tablinks"
    onclick="openTab(event, 'mbox', 'Args')">
        Args
    </button>
    <button
    group="mbox"
    id="link-mbox-Effective smtp stage"
    class="tablinks"
    onclick="openTab(event, 'mbox', 'Effective smtp stage')">
        Effective smtp stage
    </button>
    <button
    group="mbox"
    id="link-mbox-Examples"
    class="tablinks"
    onclick="openTab(event, 'mbox', 'Examples')">
        Examples
    </button>
    <button
    group="mbox"
    id="link-mbox-let rules = r#""
    class="tablinks"
    onclick="openTab(event, 'mbox', 'let rules = r#"')">
        let rules = r#"
    </button>
    <button
    group="mbox"
    id="link-mbox-     action "rm default value" || {"
    class="tablinks"
    onclick="openTab(event, 'mbox', '     action "rm default value" || {')">
             action "rm default value" || {
    </button>
    <button
    group="mbox"
    id="link-mbox-       envelop::rm_rcpt("recipient@testserver.com");"
    class="tablinks"
    onclick="openTab(event, 'mbox', '       envelop::rm_rcpt("recipient@testserver.com");')">
               envelop::rm_rcpt("recipient@testserver.com");
    </button>
    <button
    group="mbox"
    id="link-mbox-     },"
    class="tablinks"
    onclick="openTab(event, 'mbox', '     },')">
             },
    </button>
    <button
    group="mbox"
    id="link-mbox-"#;"
    class="tablinks"
    onclick="openTab(event, 'mbox', '"#;')">
        "#;
    </button>
    <button
    group="mbox"
    id="link-mbox-let states = vsmtp_test::vsl::run("
    class="tablinks"
    onclick="openTab(event, 'mbox', 'let states = vsmtp_test::vsl::run(')">
        let states = vsmtp_test::vsl::run(
    </button>
    <button
    group="mbox"
    id="link-mbox-|builder| Ok(builder"
    class="tablinks"
    onclick="openTab(event, 'mbox', '|builder| Ok(builder')">
        |builder| Ok(builder
    </button>
    <button
    group="mbox"
    id="link-mbox-  .add_root_filter_rules("#{}")?"
    class="tablinks"
    onclick="openTab(event, 'mbox', '  .add_root_filter_rules("#{}")?')">
          .add_root_filter_rules("#{}")?
    </button>
    <button
    group="mbox"
    id="link-mbox-     .add_domain_rules("testserver.com".parse().unwrap())"
    class="tablinks"
    onclick="openTab(event, 'mbox', '     .add_domain_rules("testserver.com".parse().unwrap())')">
             .add_domain_rules("testserver.com".parse().unwrap())
    </button>
    <button
    group="mbox"
    id="link-mbox-       .with_incoming(rules)?"
    class="tablinks"
    onclick="openTab(event, 'mbox', '       .with_incoming(rules)?')">
               .with_incoming(rules)?
    </button>
    <button
    group="mbox"
    id="link-mbox-       .with_outgoing(rules)?"
    class="tablinks"
    onclick="openTab(event, 'mbox', '       .with_outgoing(rules)?')">
               .with_outgoing(rules)?
    </button>
    <button
    group="mbox"
    id="link-mbox-       .with_internal(rules)?"
    class="tablinks"
    onclick="openTab(event, 'mbox', '       .with_internal(rules)?')">
               .with_internal(rules)?
    </button>
    <button
    group="mbox"
    id="link-mbox-     .build()"
    class="tablinks"
    onclick="openTab(event, 'mbox', '     .build()')">
             .build()
    </button>
    <button
    group="mbox"
    id="link-mbox-  .build()));"
    class="tablinks"
    onclick="openTab(event, 'mbox', '  .build()));')">
          .build()));
    </button>
    <button
    group="mbox"
    id="link-mbox-assert_eq!(states[&vsmtp_rule_engine::ExecutionStage::RcptTo].2, vsmtp_common::status::Status::Next);"
    class="tablinks"
    onclick="openTab(event, 'mbox', 'assert_eq!(states[&vsmtp_rule_engine::ExecutionStage::RcptTo].2, vsmtp_common::status::Status::Next);')">
        assert_eq!(states[&vsmtp_rule_engine::ExecutionStage::RcptTo].2, vsmtp_common::status::Status::Next);
    </button>
    <button
    group="mbox"
    id="link-mbox-let transport = std::sync::Arc::new(vsmtp_delivery::MBox::new(None));"
    class="tablinks"
    onclick="openTab(event, 'mbox', 'let transport = std::sync::Arc::new(vsmtp_delivery::MBox::new(None));')">
        let transport = std::sync::Arc::new(vsmtp_delivery::MBox::new(None));
    </button>
    <button
    group="mbox"
    id="link-mbox-let bound = states[&vsmtp_rule_engine::ExecutionStage::RcptTo].0.delivery().unwrap().get("
    class="tablinks"
    onclick="openTab(event, 'mbox', 'let bound = states[&vsmtp_rule_engine::ExecutionStage::RcptTo].0.delivery().unwrap().get(')">
        let bound = states[&vsmtp_rule_engine::ExecutionStage::RcptTo].0.delivery().unwrap().get(
    </button>
    <button
    group="mbox"
    id="link-mbox-  &vsmtp_common::transport::WrapperSerde::Ready(transport)"
    class="tablinks"
    onclick="openTab(event, 'mbox', '  &vsmtp_common::transport::WrapperSerde::Ready(transport)')">
          &vsmtp_common::transport::WrapperSerde::Ready(transport)
    </button>
    <button
    group="mbox"
    id="link-mbox-).unwrap();"
    class="tablinks"
    onclick="openTab(event, 'mbox', ').unwrap();')">
        ).unwrap();
    </button>
    <button
    group="mbox"
    id="link-mbox-use vsmtp_common::Address;"
    class="tablinks"
    onclick="openTab(event, 'mbox', 'use vsmtp_common::Address;')">
        use vsmtp_common::Address;
    </button>
    <button
    group="mbox"
    id="link-mbox-for (addr, addr_expected) in states[&vsmtp_rule_engine::ExecutionStage::RcptTo].0.forward_paths().unwrap().iter().zip(["
    class="tablinks"
    onclick="openTab(event, 'mbox', 'for (addr, addr_expected) in states[&vsmtp_rule_engine::ExecutionStage::RcptTo].0.forward_paths().unwrap().iter().zip([')">
        for (addr, addr_expected) in states[&vsmtp_rule_engine::ExecutionStage::RcptTo].0.forward_paths().unwrap().iter().zip([
    </button>
    <button
    group="mbox"
    id="link-mbox-    "doe@example.com","
    class="tablinks"
    onclick="openTab(event, 'mbox', '    "doe@example.com",')">
            "doe@example.com",
    </button>
    <button
    group="mbox"
    id="link-mbox-    "a@example.com","
    class="tablinks"
    onclick="openTab(event, 'mbox', '    "a@example.com",')">
            "a@example.com",
    </button>
    <button
    group="mbox"
    id="link-mbox-]) {"
    class="tablinks"
    onclick="openTab(event, 'mbox', ']) {')">
        ]) {
    </button>
    <button
    group="mbox"
    id="link-mbox-  assert_eq!("
    class="tablinks"
    onclick="openTab(event, 'mbox', '  assert_eq!(')">
          assert_eq!(
    </button>
    <button
    group="mbox"
    id="link-mbox-    *addr,"
    class="tablinks"
    onclick="openTab(event, 'mbox', '    *addr,')">
            *addr,
    </button>
    <button
    group="mbox"
    id="link-mbox-    Address::new_unchecked(addr_expected.to_string())"
    class="tablinks"
    onclick="openTab(event, 'mbox', '    Address::new_unchecked(addr_expected.to_string())')">
            Address::new_unchecked(addr_expected.to_string())
    </button>
    <button
    group="mbox"
    id="link-mbox-  );"
    class="tablinks"
    onclick="openTab(event, 'mbox', '  );')">
          );
    </button>
    <button
    group="mbox"
    id="link-mbox-  assert!(bound.iter().map(|(r, _)| r).any(|r| *r == *addr));"
    class="tablinks"
    onclick="openTab(event, 'mbox', '  assert!(bound.iter().map(|(r, _)| r).any(|r| *r == *addr));')">
          assert!(bound.iter().map(|(r, _)| r).any(|r| *r == *addr));
    </button>
    <button
    group="mbox"
    id="link-mbox-}"
    class="tablinks"
    onclick="openTab(event, 'mbox', '}')">
        }
    </button></div>

<div group="mbox" id="mbox-description" style="display: block;" markdown="span" class="tabcontent">
Set the delivery method to mbox for a recipient.
After all rules are evaluated, the email will be stored
locally in the mail box of the recipient if it exists on the server.


</div>

<div group="mbox" id="mbox-Args" class="tabcontent">

* `rcpt` - the recipient to apply the method to.


</div>

<div group="mbox" id="mbox-Effective smtp stage" class="tabcontent">

All of them.


</div>

<div group="mbox" id="mbox-Examples" class="tabcontent">

```ignore
#{
    delivery: [
       action "setup mbox" || transport::mbox("john.doe@example.com"),
    ]
}
```

```

</div>

<div group="mbox" id="mbox-let rules = r#"" class="tabcontent">
#{
  rcpt: [

</div>

<div group="mbox" id="mbox-     action "rm default value" || {" class="tabcontent">

</div>

<div group="mbox" id="mbox-       envelop::rm_rcpt("recipient@testserver.com");" class="tabcontent">

</div>

<div group="mbox" id="mbox-     }," class="tabcontent">
    action "setup mbox" || {
        const doe = address("doe@example.com");
        envelop::add_rcpt(doe);
        envelop::add_rcpt("a@example.com");
        transport::mbox(doe);
        transport::mbox("a@example.com");
    },
  ],
}

</div>

<div group="mbox" id="mbox-"#;" class="tabcontent">

</div>

<div group="mbox" id="mbox-let states = vsmtp_test::vsl::run(" class="tabcontent">

</div>

<div group="mbox" id="mbox-|builder| Ok(builder" class="tabcontent">

</div>

<div group="mbox" id="mbox-  .add_root_filter_rules("#{}")?" class="tabcontent">

</div>

<div group="mbox" id="mbox-     .add_domain_rules("testserver.com".parse().unwrap())" class="tabcontent">

</div>

<div group="mbox" id="mbox-       .with_incoming(rules)?" class="tabcontent">

</div>

<div group="mbox" id="mbox-       .with_outgoing(rules)?" class="tabcontent">

</div>

<div group="mbox" id="mbox-       .with_internal(rules)?" class="tabcontent">

</div>

<div group="mbox" id="mbox-     .build()" class="tabcontent">

</div>

<div group="mbox" id="mbox-  .build()));" class="tabcontent">

</div>

<div group="mbox" id="mbox-assert_eq!(states[&vsmtp_rule_engine::ExecutionStage::RcptTo].2, vsmtp_common::status::Status::Next);" class="tabcontent">


</div>

<div group="mbox" id="mbox-let transport = std::sync::Arc::new(vsmtp_delivery::MBox::new(None));" class="tabcontent">

</div>

<div group="mbox" id="mbox-let bound = states[&vsmtp_rule_engine::ExecutionStage::RcptTo].0.delivery().unwrap().get(" class="tabcontent">

</div>

<div group="mbox" id="mbox-  &vsmtp_common::transport::WrapperSerde::Ready(transport)" class="tabcontent">

</div>

<div group="mbox" id="mbox-).unwrap();" class="tabcontent">

</div>

<div group="mbox" id="mbox-use vsmtp_common::Address;" class="tabcontent">


</div>

<div group="mbox" id="mbox-for (addr, addr_expected) in states[&vsmtp_rule_engine::ExecutionStage::RcptTo].0.forward_paths().unwrap().iter().zip([" class="tabcontent">

</div>

<div group="mbox" id="mbox-    "doe@example.com"," class="tabcontent">

</div>

<div group="mbox" id="mbox-    "a@example.com"," class="tabcontent">

</div>

<div group="mbox" id="mbox-]) {" class="tabcontent">

</div>

<div group="mbox" id="mbox-  assert_eq!(" class="tabcontent">

</div>

<div group="mbox" id="mbox-    *addr," class="tabcontent">

</div>

<div group="mbox" id="mbox-    Address::new_unchecked(addr_expected.to_string())" class="tabcontent">

</div>

<div group="mbox" id="mbox-  );" class="tabcontent">

</div>

<div group="mbox" id="mbox-  assert!(bound.iter().map(|(r, _)| r).any(|r| *r == *addr));" class="tabcontent">

</div>

<div group="mbox" id="mbox-}" class="tabcontent">
```
</div>

</div>
</br>

<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> mbox_all </h2>

```rust,ignore
fn mbox_all() -> ()
```

<div class="tab">
    <button
    group="mbox_all"
    id="link-mbox_all-description"
    class="tablinks active"
    onclick="openTab(event, 'mbox_all', 'description')">
        Description
    </button>
    <button
    group="mbox_all"
    id="link-mbox_all-Effective smtp stage"
    class="tablinks"
    onclick="openTab(event, 'mbox_all', 'Effective smtp stage')">
        Effective smtp stage
    </button>
    <button
    group="mbox_all"
    id="link-mbox_all-Examples"
    class="tablinks"
    onclick="openTab(event, 'mbox_all', 'Examples')">
        Examples
    </button>
    <button
    group="mbox_all"
    id="link-mbox_all-let rules = r#""
    class="tablinks"
    onclick="openTab(event, 'mbox_all', 'let rules = r#"')">
        let rules = r#"
    </button>
    <button
    group="mbox_all"
    id="link-mbox_all-     action "rm default value" || {"
    class="tablinks"
    onclick="openTab(event, 'mbox_all', '     action "rm default value" || {')">
             action "rm default value" || {
    </button>
    <button
    group="mbox_all"
    id="link-mbox_all-       envelop::rm_rcpt("recipient@testserver.com");"
    class="tablinks"
    onclick="openTab(event, 'mbox_all', '       envelop::rm_rcpt("recipient@testserver.com");')">
               envelop::rm_rcpt("recipient@testserver.com");
    </button>
    <button
    group="mbox_all"
    id="link-mbox_all-     },"
    class="tablinks"
    onclick="openTab(event, 'mbox_all', '     },')">
             },
    </button>
    <button
    group="mbox_all"
    id="link-mbox_all-"#;"
    class="tablinks"
    onclick="openTab(event, 'mbox_all', '"#;')">
        "#;
    </button>
    <button
    group="mbox_all"
    id="link-mbox_all-let states = vsmtp_test::vsl::run(|builder| Ok(builder"
    class="tablinks"
    onclick="openTab(event, 'mbox_all', 'let states = vsmtp_test::vsl::run(|builder| Ok(builder')">
        let states = vsmtp_test::vsl::run(|builder| Ok(builder
    </button>
    <button
    group="mbox_all"
    id="link-mbox_all-  .add_root_filter_rules("#{}")?"
    class="tablinks"
    onclick="openTab(event, 'mbox_all', '  .add_root_filter_rules("#{}")?')">
          .add_root_filter_rules("#{}")?
    </button>
    <button
    group="mbox_all"
    id="link-mbox_all-     .add_domain_rules("testserver.com".parse().unwrap())"
    class="tablinks"
    onclick="openTab(event, 'mbox_all', '     .add_domain_rules("testserver.com".parse().unwrap())')">
             .add_domain_rules("testserver.com".parse().unwrap())
    </button>
    <button
    group="mbox_all"
    id="link-mbox_all-       .with_incoming(rules)?"
    class="tablinks"
    onclick="openTab(event, 'mbox_all', '       .with_incoming(rules)?')">
               .with_incoming(rules)?
    </button>
    <button
    group="mbox_all"
    id="link-mbox_all-       .with_outgoing(rules)?"
    class="tablinks"
    onclick="openTab(event, 'mbox_all', '       .with_outgoing(rules)?')">
               .with_outgoing(rules)?
    </button>
    <button
    group="mbox_all"
    id="link-mbox_all-       .with_internal(rules)?"
    class="tablinks"
    onclick="openTab(event, 'mbox_all', '       .with_internal(rules)?')">
               .with_internal(rules)?
    </button>
    <button
    group="mbox_all"
    id="link-mbox_all-     .build()"
    class="tablinks"
    onclick="openTab(event, 'mbox_all', '     .build()')">
             .build()
    </button>
    <button
    group="mbox_all"
    id="link-mbox_all-  .build()));"
    class="tablinks"
    onclick="openTab(event, 'mbox_all', '  .build()));')">
          .build()));
    </button>
    <button
    group="mbox_all"
    id="link-mbox_all-assert_eq!(states[&vsmtp_rule_engine::ExecutionStage::RcptTo].2, vsmtp_common::status::Status::Next);"
    class="tablinks"
    onclick="openTab(event, 'mbox_all', 'assert_eq!(states[&vsmtp_rule_engine::ExecutionStage::RcptTo].2, vsmtp_common::status::Status::Next);')">
        assert_eq!(states[&vsmtp_rule_engine::ExecutionStage::RcptTo].2, vsmtp_common::status::Status::Next);
    </button>
    <button
    group="mbox_all"
    id="link-mbox_all-let transport = std::sync::Arc::new(vsmtp_delivery::MBox::new(None));"
    class="tablinks"
    onclick="openTab(event, 'mbox_all', 'let transport = std::sync::Arc::new(vsmtp_delivery::MBox::new(None));')">
        let transport = std::sync::Arc::new(vsmtp_delivery::MBox::new(None));
    </button>
    <button
    group="mbox_all"
    id="link-mbox_all-let bound = states[&vsmtp_rule_engine::ExecutionStage::RcptTo].0.delivery().unwrap().get("
    class="tablinks"
    onclick="openTab(event, 'mbox_all', 'let bound = states[&vsmtp_rule_engine::ExecutionStage::RcptTo].0.delivery().unwrap().get(')">
        let bound = states[&vsmtp_rule_engine::ExecutionStage::RcptTo].0.delivery().unwrap().get(
    </button>
    <button
    group="mbox_all"
    id="link-mbox_all-  &vsmtp_common::transport::WrapperSerde::Ready(transport)"
    class="tablinks"
    onclick="openTab(event, 'mbox_all', '  &vsmtp_common::transport::WrapperSerde::Ready(transport)')">
          &vsmtp_common::transport::WrapperSerde::Ready(transport)
    </button>
    <button
    group="mbox_all"
    id="link-mbox_all-).unwrap();"
    class="tablinks"
    onclick="openTab(event, 'mbox_all', ').unwrap();')">
        ).unwrap();
    </button>
    <button
    group="mbox_all"
    id="link-mbox_all-use vsmtp_common::Address;"
    class="tablinks"
    onclick="openTab(event, 'mbox_all', 'use vsmtp_common::Address;')">
        use vsmtp_common::Address;
    </button>
    <button
    group="mbox_all"
    id="link-mbox_all-for (addr, addr_expected) in states[&vsmtp_rule_engine::ExecutionStage::RcptTo].0.forward_paths().unwrap().iter().zip(["
    class="tablinks"
    onclick="openTab(event, 'mbox_all', 'for (addr, addr_expected) in states[&vsmtp_rule_engine::ExecutionStage::RcptTo].0.forward_paths().unwrap().iter().zip([')">
        for (addr, addr_expected) in states[&vsmtp_rule_engine::ExecutionStage::RcptTo].0.forward_paths().unwrap().iter().zip([
    </button>
    <button
    group="mbox_all"
    id="link-mbox_all-    "doe@example.com","
    class="tablinks"
    onclick="openTab(event, 'mbox_all', '    "doe@example.com",')">
            "doe@example.com",
    </button>
    <button
    group="mbox_all"
    id="link-mbox_all-    "a@example.com","
    class="tablinks"
    onclick="openTab(event, 'mbox_all', '    "a@example.com",')">
            "a@example.com",
    </button>
    <button
    group="mbox_all"
    id="link-mbox_all-]) {"
    class="tablinks"
    onclick="openTab(event, 'mbox_all', ']) {')">
        ]) {
    </button>
    <button
    group="mbox_all"
    id="link-mbox_all-  assert_eq!("
    class="tablinks"
    onclick="openTab(event, 'mbox_all', '  assert_eq!(')">
          assert_eq!(
    </button>
    <button
    group="mbox_all"
    id="link-mbox_all-    *addr,"
    class="tablinks"
    onclick="openTab(event, 'mbox_all', '    *addr,')">
            *addr,
    </button>
    <button
    group="mbox_all"
    id="link-mbox_all-    Address::new_unchecked(addr_expected.to_string())"
    class="tablinks"
    onclick="openTab(event, 'mbox_all', '    Address::new_unchecked(addr_expected.to_string())')">
            Address::new_unchecked(addr_expected.to_string())
    </button>
    <button
    group="mbox_all"
    id="link-mbox_all-  );"
    class="tablinks"
    onclick="openTab(event, 'mbox_all', '  );')">
          );
    </button>
    <button
    group="mbox_all"
    id="link-mbox_all-  assert!(bound.iter().map(|(r, _)| r).any(|r| *r == *addr));"
    class="tablinks"
    onclick="openTab(event, 'mbox_all', '  assert!(bound.iter().map(|(r, _)| r).any(|r| *r == *addr));')">
          assert!(bound.iter().map(|(r, _)| r).any(|r| *r == *addr));
    </button>
    <button
    group="mbox_all"
    id="link-mbox_all-}"
    class="tablinks"
    onclick="openTab(event, 'mbox_all', '}')">
        }
    </button></div>

<div group="mbox_all" id="mbox_all-description" style="display: block;" markdown="span" class="tabcontent">
Set the delivery method to mbox for all recipients.
After all rules are evaluated, the email will be stored
locally in the mail box of all recipients if they exists on the server.


</div>

<div group="mbox_all" id="mbox_all-Effective smtp stage" class="tabcontent">

All of them.


</div>

<div group="mbox_all" id="mbox_all-Examples" class="tabcontent">

```ignore
#{
    delivery: [
       action "setup mbox" || transport::mbox_all(),
    ]
}
```

```

</div>

<div group="mbox_all" id="mbox_all-let rules = r#"" class="tabcontent">
#{
  rcpt: [

</div>

<div group="mbox_all" id="mbox_all-     action "rm default value" || {" class="tabcontent">

</div>

<div group="mbox_all" id="mbox_all-       envelop::rm_rcpt("recipient@testserver.com");" class="tabcontent">

</div>

<div group="mbox_all" id="mbox_all-     }," class="tabcontent">
    action "setup mbox" || {
        const doe = address("doe@example.com");
        envelop::add_rcpt(doe);
        envelop::add_rcpt("a@example.com");
        transport::mbox_all();
    },
  ],
}

</div>

<div group="mbox_all" id="mbox_all-"#;" class="tabcontent">

</div>

<div group="mbox_all" id="mbox_all-let states = vsmtp_test::vsl::run(|builder| Ok(builder" class="tabcontent">

</div>

<div group="mbox_all" id="mbox_all-  .add_root_filter_rules("#{}")?" class="tabcontent">

</div>

<div group="mbox_all" id="mbox_all-     .add_domain_rules("testserver.com".parse().unwrap())" class="tabcontent">

</div>

<div group="mbox_all" id="mbox_all-       .with_incoming(rules)?" class="tabcontent">

</div>

<div group="mbox_all" id="mbox_all-       .with_outgoing(rules)?" class="tabcontent">

</div>

<div group="mbox_all" id="mbox_all-       .with_internal(rules)?" class="tabcontent">

</div>

<div group="mbox_all" id="mbox_all-     .build()" class="tabcontent">

</div>

<div group="mbox_all" id="mbox_all-  .build()));" class="tabcontent">

</div>

<div group="mbox_all" id="mbox_all-assert_eq!(states[&vsmtp_rule_engine::ExecutionStage::RcptTo].2, vsmtp_common::status::Status::Next);" class="tabcontent">


</div>

<div group="mbox_all" id="mbox_all-let transport = std::sync::Arc::new(vsmtp_delivery::MBox::new(None));" class="tabcontent">

</div>

<div group="mbox_all" id="mbox_all-let bound = states[&vsmtp_rule_engine::ExecutionStage::RcptTo].0.delivery().unwrap().get(" class="tabcontent">

</div>

<div group="mbox_all" id="mbox_all-  &vsmtp_common::transport::WrapperSerde::Ready(transport)" class="tabcontent">

</div>

<div group="mbox_all" id="mbox_all-).unwrap();" class="tabcontent">


</div>

<div group="mbox_all" id="mbox_all-use vsmtp_common::Address;" class="tabcontent">

</div>

<div group="mbox_all" id="mbox_all-for (addr, addr_expected) in states[&vsmtp_rule_engine::ExecutionStage::RcptTo].0.forward_paths().unwrap().iter().zip([" class="tabcontent">

</div>

<div group="mbox_all" id="mbox_all-    "doe@example.com"," class="tabcontent">

</div>

<div group="mbox_all" id="mbox_all-    "a@example.com"," class="tabcontent">

</div>

<div group="mbox_all" id="mbox_all-]) {" class="tabcontent">

</div>

<div group="mbox_all" id="mbox_all-  assert_eq!(" class="tabcontent">

</div>

<div group="mbox_all" id="mbox_all-    *addr," class="tabcontent">

</div>

<div group="mbox_all" id="mbox_all-    Address::new_unchecked(addr_expected.to_string())" class="tabcontent">

</div>

<div group="mbox_all" id="mbox_all-  );" class="tabcontent">

</div>

<div group="mbox_all" id="mbox_all-  assert!(bound.iter().map(|(r, _)| r).any(|r| *r == *addr));" class="tabcontent">

</div>

<div group="mbox_all" id="mbox_all-}" class="tabcontent">
```
</div>

</div>
</br>

<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> maildir </h2>

```rust,ignore
fn maildir(rcpt: String) -> ()
fn maildir(rcpt: SharedObject) -> ()
```

<div class="tab">
    <button
    group="maildir"
    id="link-maildir-description"
    class="tablinks active"
    onclick="openTab(event, 'maildir', 'description')">
        Description
    </button>
    <button
    group="maildir"
    id="link-maildir-Args"
    class="tablinks"
    onclick="openTab(event, 'maildir', 'Args')">
        Args
    </button>
    <button
    group="maildir"
    id="link-maildir-Effective smtp stage"
    class="tablinks"
    onclick="openTab(event, 'maildir', 'Effective smtp stage')">
        Effective smtp stage
    </button>
    <button
    group="maildir"
    id="link-maildir-Examples"
    class="tablinks"
    onclick="openTab(event, 'maildir', 'Examples')">
        Examples
    </button>
    <button
    group="maildir"
    id="link-maildir-let rules = r#""
    class="tablinks"
    onclick="openTab(event, 'maildir', 'let rules = r#"')">
        let rules = r#"
    </button>
    <button
    group="maildir"
    id="link-maildir-     action "rm default value" || {"
    class="tablinks"
    onclick="openTab(event, 'maildir', '     action "rm default value" || {')">
             action "rm default value" || {
    </button>
    <button
    group="maildir"
    id="link-maildir-       envelop::rm_rcpt("recipient@testserver.com");"
    class="tablinks"
    onclick="openTab(event, 'maildir', '       envelop::rm_rcpt("recipient@testserver.com");')">
               envelop::rm_rcpt("recipient@testserver.com");
    </button>
    <button
    group="maildir"
    id="link-maildir-     },"
    class="tablinks"
    onclick="openTab(event, 'maildir', '     },')">
             },
    </button>
    <button
    group="maildir"
    id="link-maildir-"#;"
    class="tablinks"
    onclick="openTab(event, 'maildir', '"#;')">
        "#;
    </button>
    <button
    group="maildir"
    id="link-maildir-let states = vsmtp_test::vsl::run(|builder| Ok(builder"
    class="tablinks"
    onclick="openTab(event, 'maildir', 'let states = vsmtp_test::vsl::run(|builder| Ok(builder')">
        let states = vsmtp_test::vsl::run(|builder| Ok(builder
    </button>
    <button
    group="maildir"
    id="link-maildir-  .add_root_filter_rules("#{}")?"
    class="tablinks"
    onclick="openTab(event, 'maildir', '  .add_root_filter_rules("#{}")?')">
          .add_root_filter_rules("#{}")?
    </button>
    <button
    group="maildir"
    id="link-maildir-     .add_domain_rules("testserver.com".parse().unwrap())"
    class="tablinks"
    onclick="openTab(event, 'maildir', '     .add_domain_rules("testserver.com".parse().unwrap())')">
             .add_domain_rules("testserver.com".parse().unwrap())
    </button>
    <button
    group="maildir"
    id="link-maildir-       .with_incoming(rules)?"
    class="tablinks"
    onclick="openTab(event, 'maildir', '       .with_incoming(rules)?')">
               .with_incoming(rules)?
    </button>
    <button
    group="maildir"
    id="link-maildir-       .with_outgoing(rules)?"
    class="tablinks"
    onclick="openTab(event, 'maildir', '       .with_outgoing(rules)?')">
               .with_outgoing(rules)?
    </button>
    <button
    group="maildir"
    id="link-maildir-       .with_internal(rules)?"
    class="tablinks"
    onclick="openTab(event, 'maildir', '       .with_internal(rules)?')">
               .with_internal(rules)?
    </button>
    <button
    group="maildir"
    id="link-maildir-     .build()"
    class="tablinks"
    onclick="openTab(event, 'maildir', '     .build()')">
             .build()
    </button>
    <button
    group="maildir"
    id="link-maildir-  .build()));"
    class="tablinks"
    onclick="openTab(event, 'maildir', '  .build()));')">
          .build()));
    </button>
    <button
    group="maildir"
    id="link-maildir-assert_eq!(states[&vsmtp_rule_engine::ExecutionStage::RcptTo].2, vsmtp_common::status::Status::Next);"
    class="tablinks"
    onclick="openTab(event, 'maildir', 'assert_eq!(states[&vsmtp_rule_engine::ExecutionStage::RcptTo].2, vsmtp_common::status::Status::Next);')">
        assert_eq!(states[&vsmtp_rule_engine::ExecutionStage::RcptTo].2, vsmtp_common::status::Status::Next);
    </button>
    <button
    group="maildir"
    id="link-maildir-use vsmtp_common::Address;"
    class="tablinks"
    onclick="openTab(event, 'maildir', 'use vsmtp_common::Address;')">
        use vsmtp_common::Address;
    </button>
    <button
    group="maildir"
    id="link-maildir-let transport = std::sync::Arc::new(vsmtp_delivery::Maildir::new(None));"
    class="tablinks"
    onclick="openTab(event, 'maildir', 'let transport = std::sync::Arc::new(vsmtp_delivery::Maildir::new(None));')">
        let transport = std::sync::Arc::new(vsmtp_delivery::Maildir::new(None));
    </button>
    <button
    group="maildir"
    id="link-maildir-let bound = states[&vsmtp_rule_engine::ExecutionStage::RcptTo].0.delivery().unwrap().get("
    class="tablinks"
    onclick="openTab(event, 'maildir', 'let bound = states[&vsmtp_rule_engine::ExecutionStage::RcptTo].0.delivery().unwrap().get(')">
        let bound = states[&vsmtp_rule_engine::ExecutionStage::RcptTo].0.delivery().unwrap().get(
    </button>
    <button
    group="maildir"
    id="link-maildir-  &vsmtp_common::transport::WrapperSerde::Ready(transport)"
    class="tablinks"
    onclick="openTab(event, 'maildir', '  &vsmtp_common::transport::WrapperSerde::Ready(transport)')">
          &vsmtp_common::transport::WrapperSerde::Ready(transport)
    </button>
    <button
    group="maildir"
    id="link-maildir-).unwrap();"
    class="tablinks"
    onclick="openTab(event, 'maildir', ').unwrap();')">
        ).unwrap();
    </button>
    <button
    group="maildir"
    id="link-maildir-for (addr, addr_expected) in states[&vsmtp_rule_engine::ExecutionStage::RcptTo].0.forward_paths().unwrap().iter().zip(["
    class="tablinks"
    onclick="openTab(event, 'maildir', 'for (addr, addr_expected) in states[&vsmtp_rule_engine::ExecutionStage::RcptTo].0.forward_paths().unwrap().iter().zip([')">
        for (addr, addr_expected) in states[&vsmtp_rule_engine::ExecutionStage::RcptTo].0.forward_paths().unwrap().iter().zip([
    </button>
    <button
    group="maildir"
    id="link-maildir-    "doe@example.com","
    class="tablinks"
    onclick="openTab(event, 'maildir', '    "doe@example.com",')">
            "doe@example.com",
    </button>
    <button
    group="maildir"
    id="link-maildir-    "a@example.com","
    class="tablinks"
    onclick="openTab(event, 'maildir', '    "a@example.com",')">
            "a@example.com",
    </button>
    <button
    group="maildir"
    id="link-maildir-]) {"
    class="tablinks"
    onclick="openTab(event, 'maildir', ']) {')">
        ]) {
    </button>
    <button
    group="maildir"
    id="link-maildir-  assert_eq!("
    class="tablinks"
    onclick="openTab(event, 'maildir', '  assert_eq!(')">
          assert_eq!(
    </button>
    <button
    group="maildir"
    id="link-maildir-    *addr,"
    class="tablinks"
    onclick="openTab(event, 'maildir', '    *addr,')">
            *addr,
    </button>
    <button
    group="maildir"
    id="link-maildir-    Address::new_unchecked(addr_expected.to_string())"
    class="tablinks"
    onclick="openTab(event, 'maildir', '    Address::new_unchecked(addr_expected.to_string())')">
            Address::new_unchecked(addr_expected.to_string())
    </button>
    <button
    group="maildir"
    id="link-maildir-  );"
    class="tablinks"
    onclick="openTab(event, 'maildir', '  );')">
          );
    </button>
    <button
    group="maildir"
    id="link-maildir-  assert!(bound.iter().map(|(r, _)| r).any(|r| *r == *addr));"
    class="tablinks"
    onclick="openTab(event, 'maildir', '  assert!(bound.iter().map(|(r, _)| r).any(|r| *r == *addr));')">
          assert!(bound.iter().map(|(r, _)| r).any(|r| *r == *addr));
    </button>
    <button
    group="maildir"
    id="link-maildir-}"
    class="tablinks"
    onclick="openTab(event, 'maildir', '}')">
        }
    </button></div>

<div group="maildir" id="maildir-description" style="display: block;" markdown="span" class="tabcontent">
Set the delivery method to maildir for a recipient.
After all rules are evaluated, the email will be stored
locally in the `~/Maildir/new/` folder of the recipient's user if it exists on the server.


</div>

<div group="maildir" id="maildir-Args" class="tabcontent">

* `rcpt` - the recipient to apply the method to.


</div>

<div group="maildir" id="maildir-Effective smtp stage" class="tabcontent">

All of them.


</div>

<div group="maildir" id="maildir-Examples" class="tabcontent">
```ignore
#{
    delivery: [
       action "setup maildir" || transport::maildir("john.doe@example.com"),
    ]
}
```

```

</div>

<div group="maildir" id="maildir-let rules = r#"" class="tabcontent">
#{
  rcpt: [

</div>

<div group="maildir" id="maildir-     action "rm default value" || {" class="tabcontent">

</div>

<div group="maildir" id="maildir-       envelop::rm_rcpt("recipient@testserver.com");" class="tabcontent">

</div>

<div group="maildir" id="maildir-     }," class="tabcontent">
    action "setup maildir" || {
        const doe = address("doe@example.com");
        envelop::add_rcpt(doe);
        envelop::add_rcpt("a@example.com");
        transport::maildir(doe);
        transport::maildir("a@example.com");
    },
  ],
}

</div>

<div group="maildir" id="maildir-"#;" class="tabcontent">


</div>

<div group="maildir" id="maildir-let states = vsmtp_test::vsl::run(|builder| Ok(builder" class="tabcontent">

</div>

<div group="maildir" id="maildir-  .add_root_filter_rules("#{}")?" class="tabcontent">

</div>

<div group="maildir" id="maildir-     .add_domain_rules("testserver.com".parse().unwrap())" class="tabcontent">

</div>

<div group="maildir" id="maildir-       .with_incoming(rules)?" class="tabcontent">

</div>

<div group="maildir" id="maildir-       .with_outgoing(rules)?" class="tabcontent">

</div>

<div group="maildir" id="maildir-       .with_internal(rules)?" class="tabcontent">

</div>

<div group="maildir" id="maildir-     .build()" class="tabcontent">

</div>

<div group="maildir" id="maildir-  .build()));" class="tabcontent">

</div>

<div group="maildir" id="maildir-assert_eq!(states[&vsmtp_rule_engine::ExecutionStage::RcptTo].2, vsmtp_common::status::Status::Next);" class="tabcontent">


</div>

<div group="maildir" id="maildir-use vsmtp_common::Address;" class="tabcontent">

</div>

<div group="maildir" id="maildir-let transport = std::sync::Arc::new(vsmtp_delivery::Maildir::new(None));" class="tabcontent">

</div>

<div group="maildir" id="maildir-let bound = states[&vsmtp_rule_engine::ExecutionStage::RcptTo].0.delivery().unwrap().get(" class="tabcontent">

</div>

<div group="maildir" id="maildir-  &vsmtp_common::transport::WrapperSerde::Ready(transport)" class="tabcontent">

</div>

<div group="maildir" id="maildir-).unwrap();" class="tabcontent">

</div>

<div group="maildir" id="maildir-for (addr, addr_expected) in states[&vsmtp_rule_engine::ExecutionStage::RcptTo].0.forward_paths().unwrap().iter().zip([" class="tabcontent">

</div>

<div group="maildir" id="maildir-    "doe@example.com"," class="tabcontent">

</div>

<div group="maildir" id="maildir-    "a@example.com"," class="tabcontent">

</div>

<div group="maildir" id="maildir-]) {" class="tabcontent">

</div>

<div group="maildir" id="maildir-  assert_eq!(" class="tabcontent">

</div>

<div group="maildir" id="maildir-    *addr," class="tabcontent">

</div>

<div group="maildir" id="maildir-    Address::new_unchecked(addr_expected.to_string())" class="tabcontent">

</div>

<div group="maildir" id="maildir-  );" class="tabcontent">

</div>

<div group="maildir" id="maildir-  assert!(bound.iter().map(|(r, _)| r).any(|r| *r == *addr));" class="tabcontent">

</div>

<div group="maildir" id="maildir-}" class="tabcontent">
```
</div>

</div>
</br>

<div markdown="span" style='box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2); padding: 15px; border-radius: 5px;'>

<h2 class="func-name"> <code>fn</code> maildir_all </h2>

```rust,ignore
fn maildir_all() -> ()
```

<div class="tab">
    <button
    group="maildir_all"
    id="link-maildir_all-description"
    class="tablinks active"
    onclick="openTab(event, 'maildir_all', 'description')">
        Description
    </button>
    <button
    group="maildir_all"
    id="link-maildir_all-Effective smtp stage"
    class="tablinks"
    onclick="openTab(event, 'maildir_all', 'Effective smtp stage')">
        Effective smtp stage
    </button>
    <button
    group="maildir_all"
    id="link-maildir_all-Examples"
    class="tablinks"
    onclick="openTab(event, 'maildir_all', 'Examples')">
        Examples
    </button>
    <button
    group="maildir_all"
    id="link-maildir_all-let rules = r#""
    class="tablinks"
    onclick="openTab(event, 'maildir_all', 'let rules = r#"')">
        let rules = r#"
    </button>
    <button
    group="maildir_all"
    id="link-maildir_all-     action "rm default value" || {"
    class="tablinks"
    onclick="openTab(event, 'maildir_all', '     action "rm default value" || {')">
             action "rm default value" || {
    </button>
    <button
    group="maildir_all"
    id="link-maildir_all-       envelop::rm_rcpt("recipient@testserver.com");"
    class="tablinks"
    onclick="openTab(event, 'maildir_all', '       envelop::rm_rcpt("recipient@testserver.com");')">
               envelop::rm_rcpt("recipient@testserver.com");
    </button>
    <button
    group="maildir_all"
    id="link-maildir_all-     },"
    class="tablinks"
    onclick="openTab(event, 'maildir_all', '     },')">
             },
    </button>
    <button
    group="maildir_all"
    id="link-maildir_all-"#;"
    class="tablinks"
    onclick="openTab(event, 'maildir_all', '"#;')">
        "#;
    </button>
    <button
    group="maildir_all"
    id="link-maildir_all-let states = vsmtp_test::vsl::run(|builder| Ok(builder"
    class="tablinks"
    onclick="openTab(event, 'maildir_all', 'let states = vsmtp_test::vsl::run(|builder| Ok(builder')">
        let states = vsmtp_test::vsl::run(|builder| Ok(builder
    </button>
    <button
    group="maildir_all"
    id="link-maildir_all-  .add_root_filter_rules("#{}")?"
    class="tablinks"
    onclick="openTab(event, 'maildir_all', '  .add_root_filter_rules("#{}")?')">
          .add_root_filter_rules("#{}")?
    </button>
    <button
    group="maildir_all"
    id="link-maildir_all-     .add_domain_rules("testserver.com".parse().unwrap())"
    class="tablinks"
    onclick="openTab(event, 'maildir_all', '     .add_domain_rules("testserver.com".parse().unwrap())')">
             .add_domain_rules("testserver.com".parse().unwrap())
    </button>
    <button
    group="maildir_all"
    id="link-maildir_all-       .with_incoming(rules)?"
    class="tablinks"
    onclick="openTab(event, 'maildir_all', '       .with_incoming(rules)?')">
               .with_incoming(rules)?
    </button>
    <button
    group="maildir_all"
    id="link-maildir_all-       .with_outgoing(rules)?"
    class="tablinks"
    onclick="openTab(event, 'maildir_all', '       .with_outgoing(rules)?')">
               .with_outgoing(rules)?
    </button>
    <button
    group="maildir_all"
    id="link-maildir_all-       .with_internal(rules)?"
    class="tablinks"
    onclick="openTab(event, 'maildir_all', '       .with_internal(rules)?')">
               .with_internal(rules)?
    </button>
    <button
    group="maildir_all"
    id="link-maildir_all-     .build()"
    class="tablinks"
    onclick="openTab(event, 'maildir_all', '     .build()')">
             .build()
    </button>
    <button
    group="maildir_all"
    id="link-maildir_all-  .build()));"
    class="tablinks"
    onclick="openTab(event, 'maildir_all', '  .build()));')">
          .build()));
    </button>
    <button
    group="maildir_all"
    id="link-maildir_all-assert_eq!(states[&vsmtp_rule_engine::ExecutionStage::RcptTo].2, vsmtp_common::status::Status::Next);"
    class="tablinks"
    onclick="openTab(event, 'maildir_all', 'assert_eq!(states[&vsmtp_rule_engine::ExecutionStage::RcptTo].2, vsmtp_common::status::Status::Next);')">
        assert_eq!(states[&vsmtp_rule_engine::ExecutionStage::RcptTo].2, vsmtp_common::status::Status::Next);
    </button>
    <button
    group="maildir_all"
    id="link-maildir_all-use vsmtp_common::Address;"
    class="tablinks"
    onclick="openTab(event, 'maildir_all', 'use vsmtp_common::Address;')">
        use vsmtp_common::Address;
    </button>
    <button
    group="maildir_all"
    id="link-maildir_all-let transport = std::sync::Arc::new(vsmtp_delivery::Maildir::new(None));"
    class="tablinks"
    onclick="openTab(event, 'maildir_all', 'let transport = std::sync::Arc::new(vsmtp_delivery::Maildir::new(None));')">
        let transport = std::sync::Arc::new(vsmtp_delivery::Maildir::new(None));
    </button>
    <button
    group="maildir_all"
    id="link-maildir_all-let bound = states[&vsmtp_rule_engine::ExecutionStage::RcptTo].0.delivery().unwrap().get("
    class="tablinks"
    onclick="openTab(event, 'maildir_all', 'let bound = states[&vsmtp_rule_engine::ExecutionStage::RcptTo].0.delivery().unwrap().get(')">
        let bound = states[&vsmtp_rule_engine::ExecutionStage::RcptTo].0.delivery().unwrap().get(
    </button>
    <button
    group="maildir_all"
    id="link-maildir_all-  &vsmtp_common::transport::WrapperSerde::Ready(transport)"
    class="tablinks"
    onclick="openTab(event, 'maildir_all', '  &vsmtp_common::transport::WrapperSerde::Ready(transport)')">
          &vsmtp_common::transport::WrapperSerde::Ready(transport)
    </button>
    <button
    group="maildir_all"
    id="link-maildir_all-).unwrap();"
    class="tablinks"
    onclick="openTab(event, 'maildir_all', ').unwrap();')">
        ).unwrap();
    </button>
    <button
    group="maildir_all"
    id="link-maildir_all-for (addr, addr_expected) in states[&vsmtp_rule_engine::ExecutionStage::RcptTo].0.forward_paths().unwrap().iter().zip(["
    class="tablinks"
    onclick="openTab(event, 'maildir_all', 'for (addr, addr_expected) in states[&vsmtp_rule_engine::ExecutionStage::RcptTo].0.forward_paths().unwrap().iter().zip([')">
        for (addr, addr_expected) in states[&vsmtp_rule_engine::ExecutionStage::RcptTo].0.forward_paths().unwrap().iter().zip([
    </button>
    <button
    group="maildir_all"
    id="link-maildir_all-    "doe@example.com","
    class="tablinks"
    onclick="openTab(event, 'maildir_all', '    "doe@example.com",')">
            "doe@example.com",
    </button>
    <button
    group="maildir_all"
    id="link-maildir_all-    "a@example.com","
    class="tablinks"
    onclick="openTab(event, 'maildir_all', '    "a@example.com",')">
            "a@example.com",
    </button>
    <button
    group="maildir_all"
    id="link-maildir_all-]) {"
    class="tablinks"
    onclick="openTab(event, 'maildir_all', ']) {')">
        ]) {
    </button>
    <button
    group="maildir_all"
    id="link-maildir_all-  assert_eq!("
    class="tablinks"
    onclick="openTab(event, 'maildir_all', '  assert_eq!(')">
          assert_eq!(
    </button>
    <button
    group="maildir_all"
    id="link-maildir_all-    *addr,"
    class="tablinks"
    onclick="openTab(event, 'maildir_all', '    *addr,')">
            *addr,
    </button>
    <button
    group="maildir_all"
    id="link-maildir_all-    Address::new_unchecked(addr_expected.to_string())"
    class="tablinks"
    onclick="openTab(event, 'maildir_all', '    Address::new_unchecked(addr_expected.to_string())')">
            Address::new_unchecked(addr_expected.to_string())
    </button>
    <button
    group="maildir_all"
    id="link-maildir_all-  );"
    class="tablinks"
    onclick="openTab(event, 'maildir_all', '  );')">
          );
    </button>
    <button
    group="maildir_all"
    id="link-maildir_all-  assert!(bound.iter().map(|(r, _)| r).any(|r| *r == *addr));"
    class="tablinks"
    onclick="openTab(event, 'maildir_all', '  assert!(bound.iter().map(|(r, _)| r).any(|r| *r == *addr));')">
          assert!(bound.iter().map(|(r, _)| r).any(|r| *r == *addr));
    </button>
    <button
    group="maildir_all"
    id="link-maildir_all-}"
    class="tablinks"
    onclick="openTab(event, 'maildir_all', '}')">
        }
    </button></div>

<div group="maildir_all" id="maildir_all-description" style="display: block;" markdown="span" class="tabcontent">
Set the delivery method to maildir for all recipients.
After all rules are evaluated, the email will be stored
locally in each `~/Maildir/new` folder of they respective recipient
if they exists on the server.


</div>

<div group="maildir_all" id="maildir_all-Effective smtp stage" class="tabcontent">

All of them.


</div>

<div group="maildir_all" id="maildir_all-Examples" class="tabcontent">

```ignore
#{
    delivery: [
       action "setup maildir" || transport::maildir_all(),
    ]
}
```

```

</div>

<div group="maildir_all" id="maildir_all-let rules = r#"" class="tabcontent">
#{
  rcpt: [

</div>

<div group="maildir_all" id="maildir_all-     action "rm default value" || {" class="tabcontent">

</div>

<div group="maildir_all" id="maildir_all-       envelop::rm_rcpt("recipient@testserver.com");" class="tabcontent">

</div>

<div group="maildir_all" id="maildir_all-     }," class="tabcontent">
    action "setup maildir" || {
        const doe = address("doe@example.com");
        envelop::add_rcpt(doe);
        envelop::add_rcpt("a@example.com");
        transport::maildir_all();
    },
  ],
}

</div>

<div group="maildir_all" id="maildir_all-"#;" class="tabcontent">


</div>

<div group="maildir_all" id="maildir_all-let states = vsmtp_test::vsl::run(|builder| Ok(builder" class="tabcontent">

</div>

<div group="maildir_all" id="maildir_all-  .add_root_filter_rules("#{}")?" class="tabcontent">

</div>

<div group="maildir_all" id="maildir_all-     .add_domain_rules("testserver.com".parse().unwrap())" class="tabcontent">

</div>

<div group="maildir_all" id="maildir_all-       .with_incoming(rules)?" class="tabcontent">

</div>

<div group="maildir_all" id="maildir_all-       .with_outgoing(rules)?" class="tabcontent">

</div>

<div group="maildir_all" id="maildir_all-       .with_internal(rules)?" class="tabcontent">

</div>

<div group="maildir_all" id="maildir_all-     .build()" class="tabcontent">

</div>

<div group="maildir_all" id="maildir_all-  .build()));" class="tabcontent">

</div>

<div group="maildir_all" id="maildir_all-assert_eq!(states[&vsmtp_rule_engine::ExecutionStage::RcptTo].2, vsmtp_common::status::Status::Next);" class="tabcontent">


</div>

<div group="maildir_all" id="maildir_all-use vsmtp_common::Address;" class="tabcontent">

</div>

<div group="maildir_all" id="maildir_all-let transport = std::sync::Arc::new(vsmtp_delivery::Maildir::new(None));" class="tabcontent">

</div>

<div group="maildir_all" id="maildir_all-let bound = states[&vsmtp_rule_engine::ExecutionStage::RcptTo].0.delivery().unwrap().get(" class="tabcontent">

</div>

<div group="maildir_all" id="maildir_all-  &vsmtp_common::transport::WrapperSerde::Ready(transport)" class="tabcontent">

</div>

<div group="maildir_all" id="maildir_all-).unwrap();" class="tabcontent">


</div>

<div group="maildir_all" id="maildir_all-for (addr, addr_expected) in states[&vsmtp_rule_engine::ExecutionStage::RcptTo].0.forward_paths().unwrap().iter().zip([" class="tabcontent">

</div>

<div group="maildir_all" id="maildir_all-    "doe@example.com"," class="tabcontent">

</div>

<div group="maildir_all" id="maildir_all-    "a@example.com"," class="tabcontent">

</div>

<div group="maildir_all" id="maildir_all-]) {" class="tabcontent">

</div>

<div group="maildir_all" id="maildir_all-  assert_eq!(" class="tabcontent">

</div>

<div group="maildir_all" id="maildir_all-    *addr," class="tabcontent">

</div>

<div group="maildir_all" id="maildir_all-    Address::new_unchecked(addr_expected.to_string())" class="tabcontent">

</div>

<div group="maildir_all" id="maildir_all-  );" class="tabcontent">

</div>

<div group="maildir_all" id="maildir_all-  assert!(bound.iter().map(|(r, _)| r).any(|r| *r == *addr));" class="tabcontent">

</div>

<div group="maildir_all" id="maildir_all-}" class="tabcontent">
```
</div>

</div>
</br>
