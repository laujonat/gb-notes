---
description: Basic overview of IPv4 and IPv6
---

# Protocols

## What is IPv4 and IPv6?

### IPv4

IP \(version 4\) addresses are 32-bit integers that can be expressed in hexadecimal notation. The more common format, known as dotted quad or dotted decimal, is x.x.x.x, where each x can be any value between 0 and 255. For example, 192.0.2.146 is a valid IPv4 address.

![](../.gitbook/assets/image%20%281%29.png)

### IPv6

[https://techoverflow.net/2018/06/09/how-to-ssh-to-an-ipv6-address/](https://techoverflow.net/2018/06/09/how-to-ssh-to-an-ipv6-address/)

IPv6 addresses have two logical parts: a 64-bit network prefix, and a 64-bit host address part. \(The host address is often automatically generated from the interface MAC address.\[37\]\) An IPv6 address is represented by 8 groups of 16-bit hexadecimal values separated by colons \(:\) shown as follows:



## Linux Utilities

```bash
ipv6() { 
   i = ifconfig en0 | grep inet6 
   echo $i | awk -F " " '{print $2}' | sed 's/%en0//' 
}
```



{% embed url="http://www.steves-internet-guide.com/ipv6-guide/" %}

{% embed url="https://www.techrepublic.com/blog/data-center/breaking-down-an-ipv6-address-what-it-all-means/" %}

{% embed url="https://bluecatnetworks.com/glossary/what-is-ipv4/" %}



