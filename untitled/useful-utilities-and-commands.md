---
description: >-
  A process refers to a program in execution; it’s a running instance of a
  program. It is made up of the program instruction, data read from files, other
  programs or input from a system user.
---

# Process Management

## Viewing Active Processes

The `ps` utility displays a header line, followed by lines containing information about all of your processes that have controlling terminals. 

The following command outputs process information for some user.  Breaking down each column:

```bash
$ ps aux | grep ssh
```

| USER | PID | %CPU | %MEM | VSZ | RSS | TTY | STAT | START | TIME | COMMAND |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| `tim` | `1` | `0.1` | `0.0` | `226444` | `110220` | `?` | `Ssl` | `Feb03` | `25:17` | `sshd: jon@pts/8` |

* **USER** = User owning the process
* **PID** = Process ID of the process
* **%CPU** = CPU time used divided by the time the process has been running.
* **%MEM** = Ratio of the process’s resident set size to the physical memory on the machine
* **VSZ** = Virtual memory usage of entire process \(in KiB\)
* **RSS** = Resident set size, the non-swapped physical memory that a task has used \(in KiB\)
* **TTY** = Controlling tty \(terminal\)
* **STAT** = Multi-character process state
* **START** = Starting time or date of the process
* **TIME** = Cumulative CPU time
* **COMMAND** = Command that started the process with all its arguments

### Process State

To find the state of a current process, the ps utility outputs process state codes in the  `STAT` column. 

```text
D Uninterruptible sleep (usually IO)
R Running or runnable (on run queue)
S Interruptible sleep (waiting for an event to complete)
T Stopped, either by a job control signal or because it is being traced.
W paging (not valid since the 2.6.xx kernel)
X dead (should never be seen)
Z Defunct ("zombie") process, terminated but not reaped by its parent.
```

```text
< high-priority (not nice to other users)
N low-priority (nice to other users)
L has pages locked into memory (for real-time and custom IO)
s is a session leader
l is multi-threaded (using CLONE_THREAD, like NPTL pthreads do)
+ is in the foreground process group 
```

### Listing Processes

```bash
# ps = process status
# a = show processes for all users 
# u = display the process's user/owner 
# x = also show processes not attached to a terminal

$ ps aux
```

* SSH in and then use the ps command to list running processes in conjunction with the `(grep|egrep)` command to filter that result list down to what you need.

```bash
$ ps aux | egrep <thing>
```

* For example, connect to `localhost` with `ssh`. Running our command, we can see a user is connected to our local system. 

```bash
$ ssh localhost
Last login: Sat Sep  7 22:49:42 2019

$ ps aux | egrep ssh
user  74065   0.3  0.0  4258648    208 s011  R+   11:13PM   0:00.00 egrep ssh
user  30622   0.0  0.0  4381564   1148   ??  S     6:50PM   0:00.23 sshd: user@ttys011
root  30569   0.0  0.0  4325312   5984   ??  Ss    6:49PM   0:00.05 sshd: user[priv]
user  30568   0.0  0.0  4396884   5876 s007  S+    6:49PM   0:00.27 ssh localhost
```

### Killing Processes

* `ps aux` outputs the process identifier `PID` in the second column.

```bash
$ kill 30568 # kill user ssh localhost process
```

* Kill multiple `ssh-agent` processes.

```bash
$ ps aux | grep 'ssh-agent' | awk '{print $2}' | xargs kill -9
```

* Use `killall` to kill all processes by name. 
  * You can perform a specified action such as `--older-than <unix-time>`

```bash
killall $(ps aux | grep ssh | awk '{print $2}') —older-than 1w
```

#### **Source**

* [https://www.tecmint.com/linux-process-management/](https://www.tecmint.com/linux-process-management/)

