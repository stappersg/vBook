# Configuring vSMTP

vSMTP, by default, stores it's configuration in the `/etc/vsmtp` directory. Lets look at how files are organized.

## Overview

A typical vSMTP configuration looks like the following.

```
{{#include config-file-struct/hierarchy.txt}}
```
<p class="ann"> typical vSMTP configuration placed in the `/etc/vsmtp` directory</p>

Lets break it down step by step, by building a configuration from scratch.