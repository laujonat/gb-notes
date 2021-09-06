---
description: >-
  An SSH client allows you to connect to a remote computer running an SSH
  server. You can connect to a remote machine using the IPv4 or IPv6 addresses
  with their respective hostname(s).
---

# Establishing Connections

An **SSH** client allows you to **connect** to a remote computer running an **SSH** server. 

You can connect to a remote machine using the IPv4 or IPv6 addresses with their respective hostname\(s\).  

## Establishing Remote Connections

Go through `known_hosts` and `authorized_hosts`



Display internet addresses and their interface assignments.  

```bash
$ ifconfig | egrep inet
	inet 127.0.0.1 netmask 0xff000000
	inet6 ::1 prefixlen 128
	inet6 fe80::1%lo0 prefixlen 64 scopeid 0x1
	inet6 fe80::xxx:48ff:fe00:1111%en6 prefixlen 64 scopeid 0x8
	inet6 fe80::14ad:7ea2:bd9:979%en0 prefixlen 64 secured scopeid 0xa
	inet 122.11.11.10 netmask 0xfffffe00 broadcast 172.31.99.255
	inet6 fe80::xxxx:1ff:febc:bda7%awdl0 prefixlen 64 scopeid 0xc
	inet6 fe80::xxxx:8888:d115:3b%utun0 prefixlen 64 scopeid 0x12
	inet 172.20.182.112 --> 172.20.182.112 netmask 0xfffff000
	inet6 fe80::aaaa:xxxx:fe00:1122%utun1 prefixlen 64 scopeid 0x14
	inet6 3333:21d:x181:3333::11a3 prefixlen 128
```



#### IPV4 Address

```bash
inet 172.20.182.112 --> 172.20.182.112 netmask 0xfffff000
```

#### IPV6 Addresses

IPv6 addresses begin with `fe80::`

```bash
$ ssh <username>@<ipv6 address>%<interface>
```

```bash
$ ssh user@fe80::21b:21ff:fe22:e865%eth0
```



