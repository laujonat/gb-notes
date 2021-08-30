---
description: Adding Users to Linux
---

# Adding Users

### How to Create a New User in Linux <a id="how-to-create-a-new-user-in-linux"></a>

To create a new user account, invoke the `useradd` command followed by the name of the user.

For example to create a new user named `username` you would run:

### `useradd` Command <a id="useradd-command"></a>

The general syntax for the `useradd` command is as follows:

```text
useradd [OPTIONS] USERNAME
```

Only root or users with [sudo](https://linuxize.com/post/sudo-command-in-linux/) privileges can use the `useradd` command to create new user accounts.

When invoked, `useradd` creates a new user account according to the options specified on the command line and the default values set in the `/etc/default/useradd` file.

The variables defined in this file differ from distribution to distribution, which causes the `useradd` command to produce different results on different systems.

### How to Create a New User in Linux <a id="how-to-create-a-new-user-in-linux"></a>

To create a new user account, invoke the `useradd` command followed by the name of the user.

For example to create a new user named `username` you would run:

```text
sudo useradd usernameCopy
```

When executed without any option, `useradd` creates a new user account using the default settings specified in the `/etc/default/useradd` file.

The command adds an entry to the `/etc/passwd`, [`/etc/shadow,`](https://linuxize.com/post/etc-shadow-file/) `/etc/group` and `/etc/gshadow` files.

To be able to log in as the newly created user, you need to set the user password. To do that run the [`passwd`](https://linuxize.com/post/how-to-change-user-password-in-linux/) command followed by the username:

```text
sudo passwd usernameCopy
```

You will be prompted to enter and confirm the password. Make sure you use a strong password.



### How to Add a New User and Create Home Directory <a id="how-to-add-a-new-user-and-create-home-directory"></a>

On most Linux distributions, when creating a new user account with `useradd`, the user’s home directory is not created.

Use the `-m` \(`--create-home`\) option to create the user home directory as `/home/username`:

```text
sudo useradd -m usernameCopy
```

The command above creates the new user’s home directory and copies files from `/etc/skel` directory to the user’s home directory. If you [list the files](https://linuxize.com/post/how-to-list-files-in-linux-using-the-ls-command/) in the `/home/username` directory, you will see the initialization files:

```text
ls -la /home/username/Copy
```

```text
drwxr-xr-x 2 username username 4096 Dec 11 11:23 .
drwxr-xr-x 4 root     root     4096 Dec 11 11:23 ..
-rw-r--r-- 1 username username  220 Apr  4  2018 .bash_logout
-rw-r--r-- 1 username username 3771 Apr  4  2018 .bashrc
-rw-r--r-- 1 username username  807 Apr  4  2018 .profile
Copy
```

Within the home directory, the user can write, edit and delete files and directories.

### Creating a User with Specific Home Directory <a id="creating-a-user-with-specific-home-directory"></a>

By default `useradd` creates the user’s home directory in `/home`. If you want to create the user’s home directory in other location, use the `d` \(`--home`\) option.

Here is an example showing how to create a new user named `username` with a home directory of `/opt/username`:

```text
sudo useradd -m -d /opt/username username
```

