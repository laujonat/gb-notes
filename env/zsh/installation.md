---
description: Share root zsh configuration with all users
---

# Installation

### Install `zsh` through the `apt-get` package manager.

Login as root.  

```
$ sudo apt-get install zsh
```

The first time you run `zsh` a script will be run

```text
$ zsh /usr/share/zsh/functions/Newuser/zsh-newuser-install -f
```

Make sure the user has permissions to read the file and added into the sudoers file.

```text
$ sudo chmod 744 /root/.zshrc
```

For convenience, I modified `zsh-newuser-install` by adding an additional option at start:

```text
$ curl -L git.io/antigen > antigen.zsh
$ cp /root/.zshrc $zd/.zshrc
$ source $zd/.zshrc
```

 

### Configuration Files Layout <a id="3-&#x2013;-Configuration-Files-Layout"></a>

When Z Shell starts, it sources the following files in this order:

`/etc/zsh/zshenv`  
Commands to set the global command search path and other system-wide environment variables; it should not contain commands that produce output.

`~/.zshenv`  
For per-user configuration. Generally used for setting some useful environment variables.

`/etc/zsh/zprofile`  
This is a global configuration file, usually used for executing some general commands at login. On Arch Linux, by default it contains one line which sources the /etc/profile.

`/etc/profile`  
This file should be sourced by all Bourne-compatible shells upon login: it sets up an environment upon login and application-specific settings. Again on Arch Linux, Z Shell will also source this by default.

`~/.zprofile`  
This file is generally used for automatic execution of user scripts upon login.

`/etc/zsh/zshrc`  
Another global configuration file.

`~/.zshrc`  
The main user configuration file, and the one most often customised by users. This file is the one that will be used and changed in the next section.

`/etc/zsh/zlogin`  
Another global configuration file.

`~/.zlogin`  
Same as the previous file before it, except for individual-user configuration.

`/etc/zsh/zlogout`  
A global configuration file, will be sourced when a login shell exits.

`~/.zlogout`  
Same as the previous file before it, except for individual-user configuration.

