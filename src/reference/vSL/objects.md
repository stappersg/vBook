# Objects

Objects are declared through the "obj" keyword. Two syntax are available.
The inline syntax:

```rust,ignore
object type "name" "value";
```

```rust,ignore
object ip4 "my_host" "192.168.1.34";
object fqdn "local_domain" "foo.bar";
```

The extended syntax, allowing the use of user-defined fields:

```rust,ignore
object type "name" #{
    value: "value",
    <user_field1>: "value",
    ...
    <user_fieldn>: "value"
};
```

```rust,ignore
object ip4 "local_MDA" #{
    value: "192.168.0.34",
    color: "bbf3ab",
    description: "Internal delivery agent"
};
```

&#9998; | The last comma is not mandatory.

## Type of implemented objects

The following type of objects are supported natively:

| Type | Description | Syntax | Comments
| :--- | :--- | :--- | :---
| str | Untyped value | string | Generic variable.
| ip4 | IPv4 address | x.y.z.t | Decimal values.
| ip6 | IPv6 address | a:b:c:d:e:f:g:h | Hex values.
| rg4 | IPv4 network | x.y.z.t/rg | Decimal values.
| rg6 | IPv6 prefix | a:b:c:d:e:f:g:h/rg | Hex values.
| address | Email address | ident@fqdn | String.
| ident | Local part of an address | user | String.
| fqdn | Fully qualified domain name | my&#46;domain&#46;com | String.
| regex | Regular expression | | PERL regular expression.
| group | A group of objects | | See group section.
| file | A file of objects | Unix file | See file section.

### About files

File objects are standard Unix text files containing values delimited by CRLF.
Only one type of object is authorized and must be declared after the keyword "file:".

```rust,ignore
object file:ip4 "local_MTA" "/var/vmta/config/local_mta.txt";
```

```shell
# cat /var/vmta/config/local_mta.txt
192.168.1.10
192.168.1.12
10.3.4.240
```

### About groups

Groups are collections of objects. They can store references to other objects, store fresh objects or mix any type of object inside.

Unlike objects where fields are declared between parentheses, groups use squared brackets.

```rust,ignore
object file:address "whitelist" "./config/rules/whitelist.txt";

object group "authorizedUsers" [
  whitelist,
  object address "admin" "admin@mydomain.com",
];
```

Groups can be nested into other groups.

```rust,ignore
object group "deep-group" [
  object regex "foo-emails" "^[a-z0-9.]+@foo.com$",
  authorizedUsers,
];
```

&#9998; | When passed down into a check action, the whole group will be tested. The test stops when one of the groups content matches.
