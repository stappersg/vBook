# Trouble shooting

> This section is `Under construction`.

## No logs available (daemon mode)

Sometimes, logs do not get initialized fast enough in daemon mode, leading to vSMTP not starting on error.
To fix this, use the server with the `--no-daemon` option, it will log error messages on stderr.

```shell
$ sudo systemctl start vsmtp
$ sudo systemctl status vsmtp
# this prints a failed start status.

$ vsmtp -c /path/to/config.vsl --no-daemon
# this will print errors on stderr.
```
<p class="ann"> Running vsmtp with the `--no-daemon` flag to redirect logs to stderr </p>
