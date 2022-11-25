# Objects

Objects are used to create reusable configuration variables declared using Rhai functions. 

## Type of implemented objects

The following type of objects are supported natively:

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

## Creating objects

Objects can be created via associated constructors:

```js
const my_ipv4 = ip4("127.0.0.1");
const my_address = address("john.doe@example.com");
// ...
```

See the [TODO] module to get an extensive list of objects constructors.

### Recommandations

It is recommended to declare objects inside `.vsl` files and importing them via the `import` Rhai directive in rule files. (See the [Rhai modules](https://rhai.rs/book/language/modules/index.html) documentation for more information)

```js
// -- objects/network.vsl

// Do not forget to use the `export` keyword when declaring
// the object to make it accessible trough `import`.
export const localhost = ip4("127.0.0.1");
```

```js
// -- domain-enabled/incoming.vsl
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

Objects should be stored inside the `objects` directory of `/etc/vsmtp` if they are used into multiple rules sets.


```diff
/etc/vsmtp
  ┣ vsmtp.vsl
  ┣ conf.d/
  ┃     ┗ config.vsl
  ┣ domain-available/
  ┃     ┗ example.com/
  ┃       ┗ ...
  ┣ domain-enabled/
  ┃     ┣ incoming.vsl
  ┃     ┗ example.com -> ...
+ ┗ objects/
+       ┗ network.vsl
+       ┗ global.vsl
```

However, if objects are used in only a specific rule set, they should be stored directly in a separate file among the rule set.

```diff
/etc/vsmtp
  ┣ vsmtp.vsl
  ┣ conf.d/
  ┃     ┗ config.vsl
  ┣ domain-available/
  ┃     ┗ example.com/
+ ┃        ┣ network.vsl
  ┃        ┣ incoming.vsl
  ┃        ┣ outgoing.vsl
  ┃        ┗ internal.vsl
  ┣ domain-enabled/
  ┃     ┣ incoming.vsl
  ┃     ┗ example.com -> ...
- ┗ objects/
-       ┗ network.vsl
-       ┗ global.vsl
```

### Grouping objects

You can group objects using [Rhai Arrays](https://rhai.rs/book/language/arrays.html#arrays).

```js
const authorized_users = [
  address("admin@example.com"),
  address("foo@example.com"),
  address("bar@example.com"),
];
```

&#9998; | When used with check operators (`==`, `!=`, `in` etc ...), the whole array will be tested. The test stops when one element of the group matches, or nothing matches.


### Pre-defined objects

vSL already exposes some objects for you to use. You can check out the [Variable](api/Variables.md) file to get documentation on those objects and their use.

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

```js
export const local_MTA = file("/etc/vsmtp/config/local_mta.txt", "ip4");
```

### About codes

custom codes can be declared with the following syntax.

```js
const code554 = code(554, "Relay access denied");

// You can also create enhanced codes.
const code554_7_1 = code(554, "5.7.1", "Relay access denied");

// Use the code with rule statuses. `deny`, `info`, `accept` & `faccept` functions can take any code as parameter.
deny(code554);
deny(code554_7_1);
info(code554_7_1);
``` -->