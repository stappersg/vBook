# Time

Some objects and functions require argument of time.
Here is a list of available time scales format that you can use.


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

For reference, we use the [humantime](https://github.com/tailhook/humantime) crate to parse time.

Here is an example:

```js
service clamscan cmd = #{
    // for the `cmd` service, you can specify a timeout for the command.
    // You can use the different time scales above to specify the time.
    timeout: "10s",
    // timeout: "200usec",
    // timeout: "1minute",
    // timeout: "10000nsec",
    // ...
};
```