# Time

Some objects and functions require argument of time.
Here is a list of available time scales formats.

| Time scale   |      Expression      |
|----------|:-------------|
| nanoseconds | "nanos" / "nsec" / "ns" |
| microseconds | "usec" / "us" |
| milliseconds | "millis" / "msec" / "ms" |
| seconds | "seconds" / "second" / "secs" / "sec" / "s" |
| minutes | "minutes" / "minute" / "min" / "mins" / "m" |
| hours | "hours" / "hour" / "hr" / "hrs" / "h" |
| days | "days" / "day" / "d" |
| weeks | "weeks" / "week" / "w" |
| months | "months" / "month" / "M" |
| years | "years" / "year" / "y" |
<p class="ann"> Time scales and their expressions </p>


> For reference, the [humantime](https://github.com/tailhook/humantime) crate is used to parse time.

```rust,ignore
const my_command = cmd::build(#{
    // for the `cmd` service, a timeout for the command can be specified.
    // Use the different time scales above to specify the time.
    timeout: "10s",
    // timeout: "200usec",
    // timeout: "1minute",
    // timeout: "10000nsec",
    // ...
});
```
<p class="ann"> Declaring a service that requires a time value </p>
