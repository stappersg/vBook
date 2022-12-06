# Objects

Objects are variables that can be re-used accros your filtering scripts. They are placed in the `objects/` directory.

```diff
  /etc/vsmtp
  ┣ vsmtp.vsl
  ┣ conf.d/
  ┃     ┣ config.vsl
  ┃     ┗ *.vsl
  ┣ domain-available/
  ┃     ┗ example.com/
  ┃         ┗ ...
  ┣ domain-enabled/
  ┃     ┣ incoming.vsl
  ┃     ┗ example.com -> /etc/vsmtp/domain-available/example.com
+ ┗ objects/
+      ┣ net.vsl
+      ┗ *.vsl
```

Objects are declared using simple functions in a `.vsl` file.

```rust
export const localhost = ip4("127.0.0.1");
export const my_address = address("john.doe@example.com");
// ...
```

Then, they can be imported and used in rules.

```rust
import "objects/net" as net;

#{
  connect: [
    rule "trust localhost" || {
      if client_ip() == net::localhost {
        accept()
      } else {
        next()
      }
    }
  ]
}
```

> For more informations on objects and their usage, check out the [Objects reference](../../ref/vSL/objects.md)