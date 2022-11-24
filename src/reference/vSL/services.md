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
// -- domain-enabled/incoming.vsl
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
  ┣ domain-enabled/
  ┃     ┣ incoming.vsl
  ┃     ┗ example.com -> ...
+ ┗ services/
+       ┗ command.vsl
```