---
description: >-
  Bash is a Unix shell and command language developed as a replacement for the
  Bourne shell.  This section contains information on GNU Bash, or simply Bash.
---

# Bash

In the Bash, you can use the uppercase variable name equal to some value to set both shell and environment variables. You also have to use the export command to activate the variables for any subsequently executed commands.

**Source**

* [https://docs.oracle.com/cd/E19120-01/open.solaris/819-2379/userconcept-26/index.html](https://docs.oracle.com/cd/E19120-01/open.solaris/819-2379/userconcept-26/index.html)

### Load Order

1. `/etc/profile`
2. `~/.bash_profile`
3. `~/.bash_login`
4. `~/.profile`
5. `~/.bashrc`

* Bash scripts are executed sequentially by file precedence.  For example, if `bash_profile` does not exist, then bash will attempt to execute `bash_login`, then `profile.`
* Programmatic example:

{% tabs %}
{% tab title="exec\_order" %}
```bash
execute /etc/profile
IF ~/.bash_profile exists THEN
    execute ~/.bash_profile
ELSE
    IF ~/.bash_login exist THEN
        execute ~/.bash_login
    ELSE
        IF ~/.profile exist THEN
            execute ~/.profile
        END IF
    END IF
END IF
```
{% endtab %}

{% tab title="logout" %}
```bash
IF ~/.bash_logout exists THEN
  execute ~/.bash_logout
END IF
```
{% endtab %}
{% endtabs %}

When you logout, `~/.bash_logout` is executed

#### Source**s**

* [https://natelandau.com/my-mac-osx-bash\_profile](https://natelandau.com/my-mac-osx-bash_profile)
* [https://shreevatsa.wordpress.com/2008/03/30/zshbash-startup-files-loading-order-bashrc-zshrc-etc/](https://shreevatsa.wordpress.com/2008/03/30/zshbash-startup-files-loading-order-bashrc-zshrc-etc/)



\*\*\*\*



