---
description: Local IP address on your network
---

# Getting Local IP Address

Using the `ip addr` Command

Check your ip address with the **`ip addr`** command:

```text
ip addr
```

The system will scan your hardware, and display the status for each network adapter you have. Look for an entry that says **link/ether**. Below it, you should see one of the following:

```text
inet 192.168.0.10/24
```

```text
inet6 fe80::a00:27ff:fe76:1e71/64
```

## Using the `ifconfig` Command <a id="ftoc-heading-4"></a>

The third method to find your IP address involves using the [ifconfig command](https://phoenixnap.com/kb/centos-ifconfig). In the command line, enter the following:

```text
ifconfig
```

The system will display all network connections – including connected, disconnected, and virtual. Look for the one labeled **UP, BROADCAST, RUNNING, MULTICAST** to find your IP address. This lists both [IPv4 and IPv6 addresses](https://phoenixnap.com/blog/ipv4-vs-ipv6).

