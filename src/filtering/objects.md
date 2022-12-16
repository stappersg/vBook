# Objects

Objects are used to create reusable configuration variables declared using Rhai functions. 

| Type    | Description                 | Syntax                | Comments                 |
| :------ | :-------------------------- | :-------------------- | :----------------------- |
| ip4     | IPv4 address                | x.y.z.t               | Decimal values.          |
| ip6     | IPv6 address                | a:b:c:d:e:f:g:h       | Hex values.              |
| rg4     | IPv4 network                | x.y.z.t/rg            | Decimal values.          |
| rg6     | IPv6 prefix                 | a:b:c:d:e:f:g:h/rg    | Hex values.              |
| address | Email address               | identifier@fqdn            | String.                  |
| identifier   | Local part of an address    | user                  | String.                  |
| fqdn    | Fully qualified domain name | my&#46;domain&#46;com | String.                  |
| regex   | Regular expression          |                       | PERL regular expression. |
| file    | A file of objects           | Unix file             | See file section.        |
| code    | a custom smtp code          |                       | See code section.        |
<p class="ann"> All available objects types </p>

## Creating objects

Objects can be created via associated functions:

```rust,ignore
const my_ipv4 = ip4("127.0.0.1");
const my_address = address("john.doe@example.com");
// ...
```
<p class="ann"> Declaring objects in scripts </p>

See the [Object reference](../ref/vSL/api/fn::global::objects.md) to get an extensive list of objects constructors.

## Modules

It is recommended to declare objects inside `.vsl` files and importing them via the `import` Rhai directive in rule files.

> See the [Rhai modules](https://rhai.rs/book/language/modules/index.html) documentation for more details.

```rust,ignore
// Object are accessible trough `import` when declared with the `export` keyword.
export const localhost = ip4("127.0.0.1");
```
<p class="ann"> An object file, `objects/network.vsl` </p>

```
import "objects/network" as net;

#{
  connect: [
    rule "force accept localhost" || {
      if client_ip() == net::localhost {
        faccept();
      } else {
        next()
      }
    }
  ]
}
```
<p class="ann"> A rule in `filter.vsl` </p>

Objects should be stored inside the `objects` directory of `/etc/vsmtp` if they are used into multiple rules sets.


```diff
/etc/vsmtp
  ┣ vsmtp.vsl
  ┣ filter.vsl
  ┣ conf.d/
  ┃     ┗ config.vsl
  ┣ domain-available/
  ┃     ┗ example.com/
  ┃       ┗ ...
  ┣ domain-enabled/
  ┃     ┗ example.com -> ...
  ┗ objects/
+       ┗ network.vsl
```
<p class="ann"> Placing objects files in `/etc/vsmtp/objects/` </p>

However, if objects are used in only a specific rule set, they should be stored directly in a separate file among the rule set.

```diff
/etc/vsmtp
  ┣ vsmtp.vsl
  ┣ filter.vsl
  ┣ conf.d/
  ┃     ┗ config.vsl
  ┣ domain-available/
  ┃     ┗ example.com/
+ ┃        ┣ network-objects.vsl
  ┃        ┣ incoming.vsl
  ┃        ┣ outgoing.vsl
  ┃        ┗ internal.vsl
  ┣ domain-enabled/
  ┃     ┗ example.com -> ...
  ┗ objects/
-       ┗ network.vsl
```
<p class="ann"> Placing objects relative to a domain, renaming it to network-objects.vsl to make it clear that it is an object file </p>

### Grouping objects

You can group objects using [Rhai Arrays](https://rhai.rs/book/language/arrays.html#arrays).

```rust,ignore
const authorized_users = [
  address("admin@example.com"),
  address("foo@example.com"),
  address("bar@example.com"),
];
```
<p class="ann"> An array of email address </p>

> When used with check operators (`==`, `!=`, `in` etc ...), the whole array will be tested. The test stops when one element of the group matches, or nothing matches.

> You can group different types of objects together.

### Pre-defined objects

vSL already exposes some objects for you to use. You can check out the [Variable reference](../ref/vSL/variables.md) to get more details.

<!--
// TODO: Move the following descriptions to their corresponding doc comments.

### About files

File objects are standard text files containing values delimited by CRLF.
Only one type of object is authorized in one file.

```shell
cat /etc/vsmtp/config/local_mta.txt
# 192.168.1.10
# 192.168.1.12
# 10.3.4.240
```

```rust,ignore
export const local_MTA = file("/etc/vsmtp/config/local_mta.txt", "ip4");
```

### About codes

custom codes can be declared with the following syntax.

```rust,ignore
const code554 = code(554, "Relay access denied");

// You can also create enhanced codes.
const code554_7_1 = code(554, "5.7.1", "Relay access denied");

// Use the code with rule statuses. `deny`, `info`, `accept` & `faccept` functions can take any code as parameter.
deny(code554);
deny(code554_7_1);
info(code554_7_1);
``` -->