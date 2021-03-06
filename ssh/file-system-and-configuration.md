# Enable Logs

## **Enable syslog Logging**

* Setup a public SSH Server
* Local Port Forwarding 
* Remote Port Forwarding

Lets first check config file whether ssh logging enabled or not, use the following command:

`sudo vim /etc/ssh/sshd_config`

```text
[root@localhost ~]# cat /etc/syslog.conf | grep -i ssh
# sshlog
*.* /var/log/sshd/sshd.log
```

By default, ssh logging is enabled, if not enable then enable SSH logging we need to configure the syslog.conf by adding in /etc/syslog.conf file.

```text
*.* /var/log/sshd/sshd.log
```

When SSH server runs, it will produce the log messages in sshd.log to describe what is going on. These log messages will help the system administrator to track the system details such as who logged in and logged out and to troubleshoot the problem.

The `/etc/ssh/sshd_config` file is a system-wide configuration file for open SSH service which allows you to set options that modify the operation of the daemon. This configuration file contains keyword-value pairs and one per line with keywords being case sensitive.

**`SyslogFacility` AUTH and AUTHPRIV**

Messages received by `syslogd` are processed according to their facility which indicates a the origin of the message. Standard SyslogFacility includes KERN \(Messages from the OS Kernel\), DAEMON \(Messages from the Service or Daemon\), USER \(Messages from the user processes\), MAIL \(Messages from the email System\) and others.

By default, the facility for SSH server messages is AUTHPRIV. This choice may be changed with the SSH keyword SyslogFacility which determines the `syslog` facility code for logging SSH Messages.

Other possible values of SyslogFacility are `DAEMON`, `USER`, `AUTH`, `AUTHPRIV`, `LOCAL0`, `LOCAL1`, `LOCAL2`, `LOCAL3`, `LOCAL4`, `LOCAL5`, `LOCAL6`, and `LOCAL7`. The default is `AUTHPRIV`.

The option SyslogFacility specifies the facility code used when logging messages from `sshd`. The facility specifies the subsystem that produced the message--in our case, AUTH.

Normally, all authentication-related messages are logged with the `AUTHPRIV` \(or `AUTH`\) facility \[intended to be secure and never seen by unwanted eyes\], while normal operational messages are logged with the DAEMON facility.

**Enable Auth in sshd\_config file**

```text
[root@localhost ssh]# cat sshd_config | grep -i SyslogFacility
#SyslogFacility AUTH
SyslogFacility AUTHPRIV
```

**LogLevel**

It gives the verbosity level that is used when logging messages from sshd. The possible other values are `QUIET, FATAL, ERROR, INFO, VERBOSE, DEBUG, DEBUG1, DEBUG2` and `DEBUG3`. The default is INFO. `DEBUG` and `DEBUG1` are equivalent. `DEBUG2` and `DEBUG3` each specify higher levels of debugging the output.

If you want to record more information such as failed login attempts, then you should increase the logging level to VERBOSE.

Make sure to uncomment the below lines to enable `loglevel`.

```text
[root@localhost ssh]# cat sshd_config | grep -i LogLevel
#LogLevel INFO
[root@localhost ssh]#
```

**Now you need to Restart ssh service**

To enable the service of SSH, use the `service sshd start` command.

```text
[root@localhost ~]# service sshd start
Starting sshd: [ OK ]
```

You can use `watch` command to see live ssh log file updates.

```text
[root@localhost ~]# watch /var/log/messages
```

## Check failed ssh login

You can use any of the below commands to check failed ssh login session on Centos and Ubuntu.

```text
# grep "Failed password" /var/log/auth.log
# egrep "Failed|Failure" /var/log/auth.log
```

On Centos and Redhat

```text
# egrep "Failed|Failure" /var/log/secure
# grep "authentication failure" /var/log/secure
```

On Centos 7 and newer Linux distros using `systemd`

```text
# journalctl _SYSTEMD_UNIT=sshd.service | egrep "Failed|Failure"
```

If you had `auditd` package installed, then you can use `aureport` tool to get authentication report. To get a report for all the failed attempts made:

```text
# aureport -au -i --failed | more
```

## Conclusion

There are mainly 3 different log managers available to Linux to collect and store logs. The default is `syslog`, other two are [rsyslog](https://linoxide.com/how-to-setup-central-logging-server-using-rsyslog-on-ubuntu-20-04/) and Syslog-ng.

Newer Linux distros use systemd???s logging service, which uses Journalctl for querying and displaying logs from `journald`.

I hope you enjoyed reading this tutorial on ssh logging and please leave your thoughts on this tutorial in the below comment section.

`LogLevel INFO -> LogLevel Verbose`

Now all the details of ssh login attempts will be saved in your /var/log/auth.log file. 

