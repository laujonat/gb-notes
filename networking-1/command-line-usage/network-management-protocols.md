# Getting Public IP Address

### Public IP from Shell script

```text
#!/bin/bash

PUBLIC_IP=`wget http://ipecho.net/plain -O - -q ; echo`
echo $PUBLIC_IP
```

## Find Public IP using Linux Command

**Command 1 –**

Use `dig` command to find your public IP address. The dig command is a DNS lookup utility for Linux systems to look up your public IP address by connecting to the OpenDNS servers.

```text
dig +short myip.opendns.com @resolver1.opendns.com
```

**Command 2 –**

Use `wget` command to get your Public IP address as below example.

```text
wget http://ipecho.net/plain -O - -q ; echo
```

**Command 3,4,5 –**

Use `curl` command to get your Public address.

```text
curl ipecho.net/plain; echo
```

```text
curl icanhazip.com
```

```text
curl ifconfig.me
```

