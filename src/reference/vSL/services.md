# Services

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
    // Time allowed to execute the command.
    // Command is aborted if the timeout value is reached
    timeout: "60s",
    // The user to execute the command with. (optional)
    user: "user",
    // The group to execute the command with. (optional)
    group: "group",
    // Name of the command to execute.
    command: "command-to-execute",
    // Array of arguments to execute the command with.
    args: ["--arg1", "--arg2", "--arg3"],
};
```

See the [Time](../../start/configuration/time.md) chapter for more information on available time scale formats for the `timeout` field.

### Example

```js
service clamscan cmd = #{
    // Time allowed to execute the command. Command is aborted if reached.
    timeout: "10s",
    // Name of the command to execute.
    command: "clamscan",
    // Array of arguments to execute the command with.
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
service <name> <db:subtype> = #{
    ...
};
```

### CSV database

CSV databases are declared this way:

```js
service greylist db:csv = #{
    // The path to the csv database.
    connector: "/db/user_accounts.csv",
    // The access mode of the database. Can be:
    // `O_RDONLY`, `O_WRONLY` or `O_RDWR`.
    access: "O_RDONLY",
    // The refresh mode of the database.
    // Can be "always" (database is always refreshed once queried)
    // or "no" (database is readonly and never refreshed).
    //
    // WARNING: using the "always" option can make vsmtp really slow,
    //          because it has to pull the whole database in memory every
    //          time it is queried. Use it only if you have a small database
    //          or if the database is read only.
    refresh: "always",
    // The delimiter character used in the csv file.
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

### MySQL Database

```js
service mysql_greylist db:mysql = #{
    // the url to connect to your database.
    url: "mysql://localhost/",
    // the user to use when connecting. (optional)
    user: "guest",
    // the password for the user. (optional)
    password: "1234",
    // the number of connections to open on your database. (optional, 4 by default)
    connections: 4,
    // the time allowed to the database to send a
    // response to your query. (optional, 30s by default)
    timeout: "3s",
};

// Query & update the database.
let mysql_version = greylist.query("SELECT Version();");
// Like the csv database, the `query` function of the mysql database return
// an array of records.
//
// mysql version: ["8.0.30-0ubuntu0.22.04.1"]
print(`mysql version: ${mysql_version}`);

// Lets imagine that we use a database with a "greylist" table with a user & domain field.
// We can update the database this way:
let sender = mail_from();
greylist.query(`INSERT INTO greylist (user, domain) values (${sender.local_part}, ${sender.domain})`);
```

## The smtp type

The smtp type enables you to use the delegate directive to delegate the email to another service via the smtp protocol. The example hereunder explains how to delegate to ClamAV antivirus through its SMTP proxy (clamsmtpd).

```js
// -- service.vsl
service clamsmtpd smtp = #{
    delegator: #{
        // The service address to delegate to.
        address: "127.0.0.1:10026",
        // The time allowed between each message.
        timeout: "60s",
    },
    // The address where vsmtp will gather the results of the delegation.
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
