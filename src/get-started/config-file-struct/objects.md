# Objects

Objects are variables that can be re-used accros your filtering scripts. They are placed in the `objects/` directory.

```diff
  /etc/vsmtp
  ┣ vsmtp.vsl
  ┣ filter.vsl
  ┣ conf.d/
  ┃     ┣ config.vsl
  ┃     ┗ *.vsl
  ┣ domain-available/
  ┃     ┗ example.com/
  ┃         ┗ ...
  ┣ domain-enabled/
  ┃     ┗ example.com -> /etc/vsmtp/domain-available/example.com
+ ┗ objects/
+      ┣ net.vsl
+      ┗ *.vsl
```
<p class="ann"> Adding objects </p>

Objects are declared using simple functions in a `.vsl` file.

```rust,ignore
export const localhost = ip4("127.0.0.1");
export const my_address = address("john.doe@example.com");
// ...
```
<p class="ann"> Declaring an ip and email address using objects </p>

Then, they can be imported and used in rules.

```rust,ignore
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
<p class="ann"> import and use objects in rules to filter client ips </p>

> For more informations on objects and their usage, check out the [Objects reference](../../filtering/objects.md)