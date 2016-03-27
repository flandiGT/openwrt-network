openwrt-system
==============

configure network aspects of your openwrt system.

Role Variables
--------------

| variable name     | type                   | default | available options and examples       |
|-------------------|------------------------|---------|--------------------------------------|
| interfaces        | dict with objects      | static  | key = interface name                 |

Interface structure:

| variable name     | type                   | default | available options and examples       |
|-------------------|------------------------|---------|--------------------------------------|
| proto             | option as text         | static  | * static                             |
|                   |                        |         | * dhcp                               |
|                   |                        |         | * none = Unmanaged                   |
|                   |                        |         | * dslite = Dual-Stack Lite (RFC6333) |
|                   |                        |         | * 6in4 = IPv6-in-IPv4 (RFC4213)      |
|                   |                        |         | * 6to4 = IPv6-over-IPv4 (6to4)       |
|                   |                        |         | * 6rd = IPv6-over-IPv4 (6rd)         |
|                   |                        |         | * aiccu = AICCU (SIXXS)              |
|                   |                        |         | * dhcpv6 = DHCPv6 client             |
|                   |                        |         | * hnet = Automatic Homenet (HNCP)    |
|                   |                        |         | * ppp                                |
|                   |                        |         | * pptp                               |
|                   |                        |         | * pppoe                              |
|                   |                        |         | * pppoa = PPPoATM                    |
|                   |                        |         | * 3g = UMTS/GPRS/EV-DO               |
|                   |                        |         | * l2tp                               |
| ifname            | text                   | <empty> | Covered interface (like eth0)        |
| ipaddr            | text                   | <empty> | IP address (for static proto)        |
| netmask           | text                   | <empty> | IP netmask (for static proto)        |
| username          | text                   | <empty> | Username for PPPoE                   |
| password          | text                   | <empty> | Password for PPPoE                   |

Dependencies
------------

* openwrt-uci

Example Playbook
----------------

```
- role: openwrt-network
  interfaces:
    wan:
      proto: pppoe
      username: my_username
      password: my_password
    guest:
      ifname: eth0
      proto: static
      ipaddr: 10.0.0.1
      netmask: 255.255.255.0
```

[http://wiki.openwrt.org/doc/uci/network]: http://wiki.openwrt.org/doc/uci/network
