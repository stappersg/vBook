# Running vSMTP

Now that vSMTP is configured, here are a few options to launch an instance of the server.

## Daemon

If you installed vSMTP via the debian packages, a `vsmtp.service` file has been registered into your system.
Using `systemctl`, you can start your vsmtp instance with:

```sh
systemctl start vsmtp
```

## Source code

If you want to build vSMTP from it's source code, see the [dedicated chapter](../dev/build/source.md) to download and build the source code.

Then you can run the following command:

```sh
./target/release/vsmtp -c /etc/vsmtp/vsmtp.vsl --no-daemon --stdout
```

This commands run vSMTP in the foreground without creating the daemon and printing all logs to `stdout`. Remove or add vSMTP options as you see fit. (you can type `./target/release/vsmtp --help` to get a list of available options)

## Testing vSMTP

To test if your instance works properly, emulate a transaction with your favorite software.

Here is an example with curl with a vSMTP instance listening on localhost and port 10025.

```sh
curl -vv -k --url 'smtp://localhost:10025'                                  \                                     
    --mail-from 'john.doe@example.com' --mail-rcpt 'jenny.doe@example.com'  \
    # Provide an email to curl.
    --upload-file /tmp/mail.txt
```