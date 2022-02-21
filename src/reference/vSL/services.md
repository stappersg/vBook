## Services

External services (third-party software) features come with releases 0.9.x.

### Shell services

___vsmtp.toml___

```toml
[[rules.services]]
name = "my_srv"
type = "shell"
timeout = "15s"
command = "/usr/local/sbin/my_srv.sh"
args = "{mail}"
user = my_user
group = my_group
```

//
// args = ? {mail} ???
//

### Unix socket services

// TO DO

### TCP/IP socket services

// TO DO
