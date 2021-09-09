---
description: 'Official Documentation: https://stormssh.readthedocs.io/en/latest/usage.html'
---

# Configure Stormssh

## usage

### adding hosts

```text
$ storm add [-h]  [--id_file ID_FILE] name connection_uri
```

where `-h,` `id_file` are optional arguments.

#### Example

```text
$ storm add my_vps root@emreyilmaz.me:22
my_vps added to your ssh config. you can connect it by typing "ssh my_vps".
```

#### Example with id file:

```text
$ storm add my_vps root@emreyilmaz.me:22 –id_file=–id_file=/Users/myusername/mykey.pem my_vps 
```

You can connect it by typing `ssh my_vps`.

### Editing hosts

```text
storm edit [-h] [--id_file ID_FILE] name connection_uri
```

Where `-h`, `id_file` are optional arguments.

#### Example

```text
$ storm edit my_vps emre@emreyilmaz.me:2400
"my_vps" updated successfully.
```

### updating multiple hosts all at once using regular expressions

```text
storm update [-h] [--connection_uri CONNECTION_URI] [--id_file ID_FILE] name
```

Where `-h,` `id_file` and `connection_uri` are optional arguments.

example:

```text
$ storm update my_vps-[1-5] --o user=emre
"my_vps-[1-5]" updated successfully.
```

### deleting hosts

```text
$ storm delete name
```

example:

```text
$ storm delete my_vps
success hostname "my_vps" deleted successfully.
```

### searching hosts

```text
$ storm search git
Listing results for git:
  github -> emre@github.com:22
```

### listing hosts

```text
$ storm list
Listing hosts:
  vps -> 22@emreyilmaz.me:22
  netscaler -> root@127.0.0.1:8081
```

### deleting all hosts

```text
$ storm delete_all
all entries deleted.
```

### custom ssh config directives

storm does not wrap/cover all of the SSHConfig directives since there is a billion of them. But, other than adding it manually to your ssh config file, you can use **–o** parameter to accomplish this.

It works both add and edit sub commands.

```text
$ storm add web-prod web@webprod.com --o "StrictHostKeyChecking=no" --o "UserKnownHostsFile=/dev/null"
```

### command aliases

create a config file in `/home/$user/.stormssh/config`:

```text
{
    "aliases": {
        "add": ["create", "touch"],
        "delete": ["rm"]
    }

}
```

### Connection URI Format

* [user@server](mailto:user%40server):port \([root@server.com](mailto:root%40server.com):22\)
* server:port \(server.com:22\)
* server \(server.com\)

defaults for _user_ -&gt; `$USER`, _port_ -&gt; 22 if they are not specified.

see [ssh\_uri\_parser](https://github.com/emre/storm/blob/master/storm/ssh_uri_parser.py) for further look.

### Web UI

New in version 0.5.

you can also use the web ui instead of commandline interface:

```text
$ storm web
$ storm web 3333
$ storm web --debug
```

