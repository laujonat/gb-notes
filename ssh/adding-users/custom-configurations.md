---
description: Adding users with custom configurations
---

# Custom Configurations

\*To enable `zsh antigen` for all users see document [_**zsh installation**_](../../env/zsh/installation.md)_\*\*\*\*_

### Editing the default options used by `useradd`.

#### Method 1

The following example shows how to change the default shell from /bin/bash to /bin/ksh during user creation.

```text
Syntax: # useradd -D --shell=<SHELLNAME>

# useradd -D
GROUP=100
HOME=/home
INACTIVE=-1
EXPIRE=
SHELL=/bin/bash
SKEL=/etc/skel
[Note: The default shell is /bin/bash]

# useradd -D -s /bin/ksh

# useradd -D
GROUP=100
HOME=/home
INACTIVE=-1
EXPIRE=
SHELL=/bin/ksh
SKEL=/etc/skel
[Note: Now the default shell changed to /bin/ksh]

# adduser priya

# grep priya /etc/passwd
priya:x:512:512::/home/priya:/bin/ksh
[Note: New users are getting created with /bin/ksh]

# useradd -D -s /bin/bash
[Note: Set it back to /bin/bash, as the above is only for testing purpose]
```

#### Method 2

```text
Syntax: # useradd -s <SHELL> -m -d <HomeDir> -g <Group> UserName
```

* **-s SHELL** : Login shell for the user.
* **-m** : Create user’s home directory if it does not exist.
* **-d HomeDir** : Home directory of the user.
* **-g Group** : Group name or number of the user.
* **UserName** : Login id of the user.

