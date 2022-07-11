## Services

Services are declared using the `service` keyword.

## Commands

```js
// command service, enable vsmtp to run a command.
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

## Databases

```js
// the db service, enables you to communicate with a database.
// here we open a csv database with the 'connector' field.
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

## Smtp

```js
// -- service.vsl
// A smtp service, enables you to use the `delegate` directive
// to delegate the email to another service via smtp.
// Here we send the email to the `clamsmtpd` antivirus.
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