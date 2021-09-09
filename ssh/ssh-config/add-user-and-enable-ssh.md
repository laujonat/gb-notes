---
description: Passwordless login via SSH for DigitalOcean Droplet
---

# Add User and Enable SSH

Here are the set of commands that you need to run as root to enable ssh access.

This will setup `mynewuser` with passwordless sudo rights and the ability to ssh into the machine without a password \(using only your ssh-key\).

```text
$ adduser --system --group mynewuser
$ mkdir /home/mynewuser/.ssh
$ chmod 0700 /home/mynewuser/.ssh/
$ cp -Rfv /root/.ssh /home/mynewuser/
$ chown -Rfv mynewuser.mynewuser /home/mynewuser/.ssh
$ chown -R mynewuser:mynewuser /home/mynewuser/
$ gpasswd -a mynewuser sudo
$ echo "mynewuser ALL=(ALL) NOPASSWD: ALL" | (EDITOR="tee -a" visudo)
$ service ssh restart
$ usermod -s /bin/bash mynewuser
```

