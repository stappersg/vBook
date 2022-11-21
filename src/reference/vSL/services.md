# Services

Services are objects used to interact with third party software.

## Types of servers

The following services  are supported natively:

| Type    | Description                                                        |
| :------ | :------------------------------------------------------------------|
| cmd     | Execute a shell command from vSMTP                                 |
| smtp    | Connect and talk with third party software using the SMTP protocol |

## Creating services

Services can be created via their associated constructors:

```js
const echo_command = cmd(#{
    command: "echo",
    args: [ "-n", "executing a command from vSMTP!" ],
});
```

> See the [TODO] module to get an extensive list of services and how to use them.

### Recommandations

Services, compared to objects, use system resources like sockets or file descriptors.
Thus, constructing a service can be costly. It is HIGHLY recommended to declare them inside external `.vsl` files and import them via the `import` Rhai directive in rule files. (See the [Rhai modules](https://rhai.rs/book/language/modules/index.html) documentation for more information)

This way, services are initialized only once when vSMTP starts.

```js
// -- services/command.vsl

// Do not forget to use the `export` keyword when declaring
// the service to make it accessible trough `import`.
const echo = cmd(#{
    command: "echo",
    args: [ "-n", "executing a command from vSMTP!" ],
});
```

```js
// -- domain-available/incoming.vsl
import "services/command" as command;

#{
  connect: [
    action "use echo" || command::echo.run(),
  ]
}
```

Services should be stored inside the `services` directory of `/etc/vsmtp`.


```diff
/etc/vsmtp
  ┣ vsmtp.vsl
  ┣ conf.d/
  ┃     ┗ config.vsl
  ┣ domain-available/
  ┃     ┗ example.com/
  ┃       ┗ ...
+ ┗ services/
+       ┗ command.vsl
```
<!-- 

// TODO: move the following sections to their respective auto generated documentation.

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

Using [Rhai arrays](https://rhai.rs/book/language/arrays.html) and [maps](https://rhai.rs/book/language/object-maps.html#object-maps), vSL can easily fetch and update data from a mysql database.

Again taking previous "greylisting" as an example, a database named "greylist", with a table "sender" described as follows is created:

```console
+---------+--------------+------+-----+---------+
| Field   | Type         | Null | Key | Default |
+---------+--------------+------+-----+---------+
| address | varchar(500) | NO   | PRI | NULL    |
| user    | varchar(500) | NO   |     | NULL    |
| domain  | varchar(500) | NO   |     | NULL    |
+---------+--------------+------+-----+---------+
```

To connect to the database, create a "mysql_greylist" service of type `db:mysql`.

```js
service mysql_greylist db:mysql = #{
    // the url to connect to your database.
    url: "mysql://localhost/",
    // the number of connections to open on your database. (optional, 4 by default)
    connections: 4,
    // the time allowed to the database to send a
    // response to your query. (optional, 30s by default)
    timeout: "3s",
};
```

This service is used to query and update the database using SQL commands.

```js
// Query the database.
let senders = mysql_greylist.query("SELECT * FROM greylist.sender;");

// Like the csv database, the `query` function of the mysql database return
// an array of records, except that each record is a Rhai Map, meaning that
// you can access the record fields using their names.
//
// vSL will then return fetched records using this form:
// Array [
//     Map #{
//         "user": "john.doe",
//         "domain": "example.com",
//         "address": "john.doe@example.com",
//     },
//     Map #{
//         "user": "green",
//         "domain": "test.com",
//         "address": "green@test.com",
//     },
// ]
//
// (We assume that the "sender" table is populated with two records in the above example)
//
// To extract records and fields, use the syntax below.
print(`first sender address : ${senders[0].address}`); // will print "john.doe@example.com";
print(`second sender domain : ${senders[1].domain}`); // will print "test.com";

// We can also update the database this way:
let sender = mail_from();
mysql_greylist.query(`INSERT INTO greylist.sender (user, domain, address) values (${sender.local_part}, ${sender.domain}, ${sender.address});`);
```

## The smtp type

The smtp type allows the vSL `delegate` directive to delegate the email to another service via the smtp protocol. The example hereunder explains how to delegate to ClamAV antivirus through its SMTP proxy (clamsmtpd).

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

Check out the [Services](./api/Services.md) chapter for the full list of functions for services. -->
