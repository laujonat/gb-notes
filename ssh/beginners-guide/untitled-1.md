# SSH Agent

## Usage

* The `ssh-agent` is a helper program that keeps track of user's identity keys and their passwords. 
* The agent can then use the keys to log into other servers without having the user type in a password or passphrase again.

### `ssh-keygen`

```bash
ssh-keygen -R [hostname]
ssh-keygen -R [ip_address]
ssh-keygen -R [hostname],[ip_address]
```

### **`ssh-keyscan`**

```bash
ssh-keyscan -H [hostname],[ip_address] >> ~/.ssh/known_hosts
ssh-keyscan -H [ip_address] >> ~/.ssh/known_hosts
ssh-keyscan -H [hostname] >> ~/.ssh/known_hosts
```

**Sources**

* [https://linux.101hacks.com/unix/ssh-agent/](https://linux.101hacks.com/unix/ssh-agent/)
* [http://blog.joncairns.com/2013/12/understanding-ssh-agent-and-ssh-add/](http://blog.joncairns.com/2013/12/understanding-ssh-agent-and-ssh-add/)

