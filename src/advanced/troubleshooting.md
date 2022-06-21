# Trouble shooting

Here is a section for eventual problems that can happen during your vSMTP setup.

## No logs available (daemon mode)

Sometimes, logs do not get initialized fast enough in daemon mode, leading to vSMTP not starting on error.
To fix this, use the server with the `--no-daemon` option, this will log error messages on stderr, enabling you to get directions to fix your problem.

```shell
$ sudo systemctl start vsmtp
$ sudo systemctl status vsmtp
# this prints a failed start status.

$ vsmtp -c /path/to/config.toml --no-daemon
# this will print errors on stderr.
```