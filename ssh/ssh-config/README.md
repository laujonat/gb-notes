---
description: SSH config notes
---

# SSH Config

{% embed url="https://stormssh.readthedocs.io/en/master/" %}

`stormssh` is a command line tool to manage your `ssh` connections.

### SSH Config File Location <a id="ssh-config-file-location"></a>

OpenSSH client-side configuration file is named `config`, and it is stored in the `.ssh` directory under the user’s home directory.

### SSH Config File Structure and Patterns <a id="ssh-config-file-structure-and-patterns"></a>

The SSH Config File takes the following structure:

```text
Host hostname1
    SSH_OPTION value
    SSH_OPTION value

Host hostname2
    SSH_OPTION value

Host *
    SSH_OPTION value
```

Use `stormssh` to manage SSH config.  



