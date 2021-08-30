---
description: Cheat sheet of Linux commands
---

# CLI Commands

On Linux/Unix or Linux-like operating systems, it ships with an internal manual used to reference system commands and use cases. 

[http://www.linfo.org/man.html](http://www.linfo.org/man.html)

```bash
$ man ssh
   SSH(1) . BSD General Commands   Manual                  

NAME
   ssh -- OpenSSH SSH client (remote login program)

SYNOPSIS
   ssh [-46AaCfGgKkMNnqsTtVvXxYy] [-B bind_interface] [-b bind_address] \
    [-c cipher_spec] [-D [bind_address:]port] [-E log_file] [-e escape_char] \
    [-F configfile] [-I pkcs11] [-i identity_file] [-J destination] \
    [-L address] [-l login_name] [-m mac_spec] [-O ctl_cmd] [-o option] \
    [-p port] [-Q query_option] [-R address] [-S ctl_path] [-W host:port] \
    [-w local_tun[:remote_tun]] destination [command]
```

Instead of using Google, Bing, or your best friend, it is to your advantage to spend time understanding how to effectively utilize Linux manuals. 

Some alternatives to the default Linux man pages:

{% code title="gem \| brew \| npm \| pip " %}
```bash
$ gem install bropages
$ brew install cheat
$ npm install -g tldr
$ pip install --user manly
```
{% endcode %}

## Navigation

### Files and Directories

```bash
$ man ls 
```

####  `ls`

* `ls -lt` List sorted output by last date and time modified
* `ls -halt`- List sorted files/dir both hidden and human readable sizes
* `ls -lah` - List all hidden/non-hidden files/dir and their sizes ``

```bash
$ man pwd 
```

#### `pwd`

* `pwd` Sort output by last date and time modified
* `$ mypath=$(pwd)` - Assign current directory to an environment variable

## System Usage

### Displaying Free Disk Space

```bash
$ man df
```

#### `df`

The df utility displays statistics about the amount of free disk space on the specified filesystem or on the filesystem of which file is a part.

* `df -H` - Human readable output with unit suffixes.
* `df -h` - Use unit suffixes: Byte, Kilobyte, Megabyte, Gigabyte, Terabyte and Petabyte.
* `df -l` - Only display information about locally-mounted filesystems

### Display Disk Usage Statistics

```bash
$ man du
```

#### `du`

* `du -sh */` - Display disk usage for file, folder, directories at the current location
* `du -h <dir>` - Display human readable disk usage in human readable format

## Searching

#### `grep | egrep`

#### `awk`

```bash
NAME
awk - pattern-directed scanning and processing language

SYNOPSIS
awk [ -F fs ] [ -v var=value ] [ 'prog' | -f progfile ] [ file ... ]
```

* Awk scans each input file for lines that match any of a set of patterns specified literally in prog or in one or more files specified as `-f` profile.
* The `-F (fs)` option defines the input field separator to be the regular expression fs.
* Get hostname if you know Host, get Host if you know Hostname

```bash
$ awk -v h="172.31.98.85" '$1 == "Host" {r = $2} $1 == "Hostname" && $2 == h {print r; exit}' ~/.ssh/config
```

#### `sed`

Stream editor that reads the specified files, or the standard input if no files are specified, modifying the input as specified by a list of commands.

```bash
$ for i in $(seq 1 10); do /usr/bin/time $SHELL -i -c exit; done
```

**Source**

* [https://www.systutorials.com/docs/linux/man/1p-df/](https://www.systutorials.com/docs/linux/man/1p-df/)
* [https://unix.stackexchange.com/questions/430550/split-single-line-into-multiple-lines-newline-character-missing-for-all-the-lin](https://unix.stackexchange.com/questions/430550/split-single-line-into-multiple-lines-newline-character-missing-for-all-the-lin)

