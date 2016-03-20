openwrt-system
==============

configure network aspects of your openwrt system.

Role Variables
--------------

| variable name     | type                   | default | available options and examples       |
|-------------------|------------------------|---------|--------------------------------------|
| wan_protocol      | option as text         | static  | * static                             |
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
| wan_username      | text                   | <empty> |                                      |
| wan_password      | text                   | <empty> |                                      |

Dependencies
------------

* openwrt-uci

Example Playbook
----------------

```
- role: openwrt-network
  wan_protocol: pppoe
  wan_username: my_username
  wan_password: my_password
```

[http://wiki.openwrt.org/doc/uci/network]: http://wiki.openwrt.org/doc/uci/network
