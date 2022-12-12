# Configuring vSMTP

vSMTP, by default, stores it's configuration in the `/etc/vsmtp` directory. Lets look at how files are organized.

## Overview

A typical vSMTP configuration looks like the following.

```
/etc/vsmtp
┣ vsmtp.vsl
┣ conf.d/
┃     ┣ config.vsl
┃     ┗ *.vsl
┣ domain-available/
┃     ┣ example.com/
┃     ┃    ┣ config.vsl
┃     ┃    ┣ incoming.vsl
┃     ┃    ┣ outgoing.vsl
┃     ┃    ┗ internal.vsl
┃     ┗ test.com/
┃         ┗ ...
┣ domain-enabled/
┃     ┣ incoming.vsl
┃     ┗ example.com -> /etc/vsmtp/domain-available/example.com
┣ objects/
┃     ┣ net.vsl
┃     ┗ *.vsl
┣ services/
┃     ┣ users-ldap.vsl
┃     ┣ backup-mysql.vsl
┃     ┗ *.vsl
┗ plugins/
      ┣ mysql.so -> /usr/lib/vsmtp/libvsmtp-mysql-plugin.so
      ┗ ldap.so  -> /usr/lib/vsmtp/libvsmtp-ldap-plugin.so
```
<p class="ann"> typical vSMTP configuration placed in the `/etc/vsmtp` directory</p>

Lets break it down step by step, by building a configuration from scratch.