# Objects

Objects are declared through the "object" keyword. Two syntax are available.
The inline syntax:

```js
object <name> <type> = "<value>";
```

```js
object my_host ip4 = "192.168.1.34";
object local_domain fqdn = "foo.bar";
```

The extended syntax, allowing the use of user-defined fields:

```js
object <name> <type> = #{
    value: "value",
    <field1>: "value",
    ...
    <fieldn>: "value"
};
```

```js
object local_mda ip4 = #{
    value: "192.168.0.34",
    color: "bbf3ab",
    description: "Internal delivery agent"
};
```

&#9998; | Only the "value:" field is mandatory. The other fields are not.

## Type of implemented objects

The following type of objects are supported natively:

| Type    | Description                 | Syntax                | Comments                 |
| :------ | :-------------------------- | :-------------------- | :----------------------- |
| string  | Untyped value               | string                | Generic variable.        |
| ip4     | IPv4 address                | x.y.z.t               | Decimal values.          |
| ip6     | IPv6 address                | a:b:c:d:e:f:g:h       | Hex values.              |
| rg4     | IPv4 network                | x.y.z.t/rg            | Decimal values.          |
| rg6     | IPv6 prefix                 | a:b:c:d:e:f:g:h/rg    | Hex values.              |
| address | Email address               | identifier@fqdn            | String.                  |
| identifier   | Local part of an address    | user                  | String.                  |
| fqdn    | Fully qualified domain name | my&#46;domain&#46;com | String.                  |
| regex   | Regular expression          |                       | PERL regular expression. |
| group   | A group of objects          |                       | See group section.       |
| file    | A file of objects           | Unix file             | See file section.        |
| code    | a custom smtp code          |                       | See code section.        |

### About files

File objects are standard Unix text files containing values delimited by CRLF.
Only one type of object is authorized and must be declared after the keyword "file:".

```c
object local_MTA file:ip4 = "/etc/vsmtp/config/local_mta.txt";
```

```shell
cat /etc/vsmtp/config/local_mta.txt
# 192.168.1.10
# 192.168.1.12
# 10.3.4.240
```

### About groups

Groups are collections of objects. They can store references to other objects, store fresh objects or mix any type of object inside.

Unlike objects where fields are declared between parentheses, groups use squared brackets.

```js
object whitelist file:address = "/etc/vsmtp/config/whitelist.txt";

object authorized_users group = [
  whitelist,
  object admin address = "admin@mydomain.com",
];
```

Groups can be nested into other groups.

```js
object deep_group group = [
  object foo_emails regex = "^[a-z0-9.]+@foo.com$",
  authorizedUsers,
];
```

&#9998; | When used with check operators (`==`, `!=`, `in` etc ...), the whole group will be tested. The test stops when one of the groups content matches.

### About codes

custom codes can be declared with the following syntax.

```js
object code554_7_1 code = #{
  base: 554,
  enhanced: "5.7.1",
  text: "Relay access denied"
};

// use the code in your rules. deny or send a informational message.
deny(code554_7_1);
info(code554_7_1);
```

### Pre-defined objects

vSL already exposes some objects for you to use. You can check out the [Variable](api/Variables.md) file to get documentation on those objects and their use.