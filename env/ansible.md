---
description: Ansible can be used for automating server configuration
---

# Ansible

## Control Node Setup 

### Step 1 — Installing Ansible <a id="step-1-&#x2014;-installing-ansible"></a>

To begin using Ansible as a means of managing your server infrastructure, you need to install the Ansible software on the machine that will serve as the Ansible control node.

From your control node, run the following command to include the official project’s PPA \(personal package archive\) in your system’s list of sources:

```text
sudo apt-add-repository ppa:ansible/ansible
```

Press `ENTER` when prompted to accept the PPA addition.

Next, refresh your system’s package index so that it is aware of the packages available in the newly included PPA:

```text
sudo apt update
```

Following this update, you can install the Ansible software with:

```text
sudo apt install ansible
```

Your Ansible control node now has all of the software required to administer your hosts. Next, we will go over how to add your hosts to the control node’s inventory file so that it can control them.

### Step 2 — Setting Up the Inventory File <a id="step-2-&#x2014;-setting-up-the-inventory-file"></a>

The _inventory file_ contains information about the hosts you’ll manage with Ansible. You can include anywhere from one to several hundred servers in your inventory file, and hosts can be organized into groups and subgroups. The inventory file is also often used to set variables that will be valid only for specific hosts or groups, in order to be used within playbooks and templates. Some variables can also affect the way a playbook is run, like the `ansible_python_interpreter` variable that we’ll see in a moment.

To edit the contents of your default Ansible inventory, open the `/etc/ansible/hosts` file using your text editor of choice, on your Ansible Control Node:

```text
sudo nano /etc/ansible/hosts
```

**Note**: some Ansible installations won’t create a default inventory file. If the file doesn’t exist in your system, you can create a new file at `/etc/ansible/hosts` or provide a custom inventory path using the `-i` parameter when running commands and playbooks.  


The default inventory file provided by the Ansible installation contains a number of examples that you can use as references for setting up your inventory. The following example defines a group named `[servers]` with three different servers in it, each identified by a custom alias: **server1**, **server2**, and **server3**. Be sure to replace the highlighted IPs with the IP addresses of your Ansible hosts./etc/ansible/hosts

```text
[servers]
server1 ansible_host=203.0.113.111
server2 ansible_host=203.0.113.112
server3 ansible_host=203.0.113.113

[all:vars]
ansible_python_interpreter=/usr/bin/python3
```

The `all:vars` subgroup sets the `ansible_python_interpreter` host parameter that will be valid for all hosts included in this inventory. This parameter makes sure the remote server uses the `/usr/bin/python3` Python 3 executable instead of `/usr/bin/python` \(Python 2.7\), which is not present on recent Ubuntu versions.

When you’re finished, save and close the file by pressing `CTRL+X` then `Y` and `ENTER` to confirm your changes.

Whenever you want to check your inventory, you can run:

```text
ansible-inventory --list -y
```

You’ll see output similar to this, but containing your own server infrastructure as defined in your inventory file:

```text
Outputall:
  children:
    servers:
      hosts:
        server1:
          ansible_host: 203.0.113.111
          ansible_python_interpreter: /usr/bin/python3
        server2:
          ansible_host: 203.0.113.112
          ansible_python_interpreter: /usr/bin/python3
        server3:
          ansible_host: 203.0.113.113
          ansible_python_interpreter: /usr/bin/python3
    ungrouped: {}
```

Now that you’ve configured your inventory file, you have everything you need to test the connection to your Ansible hosts.

### Step 3 — Testing Connection <a id="step-3-&#x2014;-testing-connection"></a>

After setting up the inventory file to include your servers, it’s time to check if Ansible is able to connect to these servers and run commands via SSH.

For this guide, we will be using the Ubuntu **root** account because that’s typically the only account available by default on newly created servers. If your Ansible hosts already have a regular sudo user created, you are encouraged to use that account instead.

You can use the `-u` argument to specify the remote system user. When not provided, Ansible will try to connect as your current system user on the control node.

From your local machine or Ansible control node, run:

```text
ansible all -m ping -u root
```

 Copy

This command will use Ansible’s built-in [`ping` module](https://docs.ansible.com/ansible/latest/modules/ping_module.html) to run a connectivity test on all nodes from your default inventory, connecting as **root**. The `ping` module will test:

* if hosts are accessible;
* if you have valid SSH credentials;
* if hosts are able to run Ansible modules using Python.

You should get output similar to this:

```text
Outputserver1 | SUCCESS => {
    "changed": false, 
    "ping": "pong"
}
server2 | SUCCESS => {
    "changed": false, 
    "ping": "pong"
}
server3 | SUCCESS => {
    "changed": false, 
    "ping": "pong"
}
```

If this is the first time you’re connecting to these servers via SSH, you’ll be asked to confirm the authenticity of the hosts you’re connecting to via Ansible. When prompted, type `yes` and then hit `ENTER` to confirm.

Once you get a `"pong"` reply back from a host, it means you’re ready to run Ansible commands and playbooks on that server.

**Note**: If you are unable to get a successful response back from your servers, check our [Ansible Cheat Sheet Guide](https://www.digitalocean.com/community/tutorials/how-to-use-ansible-cheat-sheet-guide) for more information on how to run Ansible commands with different connection options.  


### Step 4 — Running Ad-Hoc Commands \(Optional\) <a id="step-4-&#x2014;-running-ad-hoc-commands-optional"></a>

After confirming that your Ansible control node is able to communicate with your hosts, you can start running ad-hoc commands and playbooks on your servers.

Any command that you would normally execute on a remote server over SSH can be run with Ansible on the servers specified in your inventory file. As an example, you can check disk usage on all servers with:

```text
ansible all -a "df -h" -u root
```

 

```text
Output
server1 | CHANGED | rc=0 >>
Filesystem      Size  Used Avail Use% Mounted on
udev            3.9G     0  3.9G   0% /dev
tmpfs           798M  624K  798M   1% /run
/dev/vda1       155G  2.3G  153G   2% /
tmpfs           3.9G     0  3.9G   0% /dev/shm
tmpfs           5.0M     0  5.0M   0% /run/lock
tmpfs           3.9G     0  3.9G   0% /sys/fs/cgroup
/dev/vda15      105M  3.6M  101M   4% /boot/efi
tmpfs           798M     0  798M   0% /run/user/0

server2 | CHANGED | rc=0 >>
Filesystem      Size  Used Avail Use% Mounted on
udev            2.0G     0  2.0G   0% /dev
tmpfs           395M  608K  394M   1% /run
/dev/vda1        78G  2.2G   76G   3% /
tmpfs           2.0G     0  2.0G   0% /dev/shm
tmpfs           5.0M     0  5.0M   0% /run/lock
tmpfs           2.0G     0  2.0G   0% /sys/fs/cgroup
/dev/vda15      105M  3.6M  101M   4% /boot/efi
tmpfs           395M     0  395M   0% /run/user/0

...
```

The highlighted command `df -h` can be replaced by any command you’d like.

You can also execute [Ansible modules](https://docs.ansible.com/ansible/latest/modules/modules_by_category.html) via ad-hoc commands, similarly to what we’ve done before with the `ping` module for testing connection. For example, here’s how we can use the `apt` module to install the latest version of `vim` on all the servers in your inventory:

```text
ansible all -m apt -a "name=vim state=latest" -u root
```

You can also target individual hosts, as well as groups and subgroups, when running Ansible commands. For instance, this is how you would check the `uptime` of every host in the `servers` group:

```text
ansible servers -a "uptime" -u root
```

 

We can specify multiple hosts by separating them with colons:

```text
ansible server1:server2 -m ping -u root
```

 

For more information on how to use Ansible, including how to execute playbooks to automate server setup, you can check our [Ansible Reference Guide](https://www.digitalocean.com/community/cheatsheets/how-to-use-ansible-cheat-sheet-guide).

