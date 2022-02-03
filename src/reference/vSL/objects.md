## Objects

Objects are declared through the "obj" keyword. Two syntax are available.
The inline syntax:

```vsl
obj type "name" "value";
```

```vsl
obj ip4 "my_host" "192.168.1.34";
obj fqdn "local_domain" "foo.bar";
```

The extended syntax, allowing the use of user-defined fields:

```vsl
obj type "name" #{
    value: "value",
    <user_field1>: "value",
    ...
    <user_fieldn>: "value",
};
```

```vsl
obj ip4 "local_MDA" #{
    value: "192.168.0.34",
    color: "bbf3ab",
    description: "Internal delivery agent"
};
```

>Note that the last comma is not mandatory.

### Type of implemented objects

The following type of objects are supported natively:

| Type | Description | Syntax | Comments
| :--- | :--- | :--- | :---
| val | Untyped value | string | Bind a value.
| ip4 | IPv4 address | x.y.z.t
| rg4 | IPv4 network | x.y.z.t/rg
| addr | email address | user@fqdn
| fqdn | Fully qualified domain name | my&#46;domain&#46;com
| regex | Regular expression | | PERL regular expression.
| grp | A group of objects | | See group section.
| file | A file of objects | Unix file | See file section.

### About files

File objects are standard Unix text files containing values delimited by CRLF.
Only one type of object is authorized and must be declared after the keyword "file:".

```vsl
obj file:ip4 "local_MTA" "/var/vmta/config/local_mta.txt";
```

```vsl
# cat /var/vmta/config/local_mta.txt
192.168.1.10
192.168.1.12
10.3.4.240
```

### About groups

Groups are collections of objects.

```vsl
obj file:addr "whitelist" "./config/rules/whitelist.txt";

obj grp "authorizedUsers" [
  whitelist,
  obj addr "admin" "admin@mydomain.com",
];

obj grp "deep-group" [
  obj regex "foo-emails" "^[a-z0-9.]+@foo.com$",
  authorizedUsers,
];
```

>Please note that unlike objects where fields are declared between parentheses, groups use squared brackets.
