# Services

`DRAFT - to be reviewed`

Services are mainly used to interact with third party software.
Services are declared using the `service` keyword, followed by its name, and its type.

```js
service <name> <type> = #{
    <field1>: "value",
    <field2>: "value",
    ...
    <fieldn>: "value"
};
```

## The command type

This type lets you execute Unix shell commands.

```js
service clamscan cmd = #{
    timeout: "10s",
    command: "clamscan",
    args: ["--infected", "--remove", "--recursive", "/home/jdoe"],
};

// run the service.
// the command executed will be:
// clamscan --infected --remove --recursive /home/jdoe
clamscan.run_cmd();
// run the service with custom arguments (based one are replaced).
// clamscan --infected /home/another
clamscan.run_cmd([ "--infected", "/home/another" ]);
```

## The database type

The db service allows connection and operations on databases. Several subtypes are available.

```js
service <name> <db::subtype> = #{
    ...
};
```

This is a csv database with the 'connector' field.

```js
service greylist db:csv = #{
    connector: "/db/user_accounts.csv",
    access: "O_RDONLY",
    refresh: "always",
    delimiter: ",",
};

// query & update the database.
let john = greylist.get("john");
greylist.set(["new", "user", "new.user@example.com"]);
greylist.rm("green");

// manipulating a record.

// ["john", "doe", "john.doe@example.com"]
print(john);

// records are stored in vsl arrays.
// to get a field in a record, simply use it's index.

// "john.doe@example.com"
print(john[2]);
```

## The smtp type

The smtp type enables you to use the delegate directive to delegate the email to another service via the smtp protocol. The example hereunder explains how to delegate to ClamAV antivirus through its SMTP proxy (clamsmtpd).

```js
// -- service.vsl
service clamsmtpd smtp = #{
    delegator: #{
        address: "127.0.0.1:10026",
        timeout: "60s",
    },
    receiver: "127.0.0.1:10024",
};

// -- main.vsl

// you cannot use `import "service" as service;` here because `service` is
// a reserved keyword.
import "service" as svc;

#{
    postq: [
        // this will delegate the email using the `clamsmtpd` service.
        delegate svc::clamsmtpd "delegate antivirus processing" || {
            // this is executed after the delegation results have been
            // received on port 10024.
            ...
        }
    ]
}
```

Check out the [Services](./api/Services.md) chapter for the full list of functions for services.
