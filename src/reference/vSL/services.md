## Services

Services are declared using the `service` keyword.

## Commands

```js
// shell service, enable vsmtp to run a command via a shell.
service clamscan shell = #{
    timeout: "10s",
    command: "clamscan",
    args: ["--infected", "--remove", "--recursive", "/home/jdoe"],
};

// run the service.
// the command executed will be:
// clamscan --infected --remove --recursive /home/jdoe
clamscan.run_shell();
// run the service with custom arguments (based one are replaced).
// clamscan --infected /home/another
clamscan.run_shell([ "--infected", "/home/another" ]);
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