openwrt-system
==============

configure network aspects of your openwrt system.

Role Variables
--------------

| variable name     | type                   | default  | available options and examples             |
|-------------------|------------------------|----------|--------------------------------------------|
| interfaces        | dict with objects      | static   | key = interface name                       |
| switch_vlans      | array with objects     | <empty>  | see attributes in object description below |

interface structure:

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

switch_vlans attributes:

| attribute name | property type         | valid values / examples                                          |
|----------------|-----------------------|------------------------------------------------------------------|
| index          | array_index as number | specify the element index in network.switch_vlans[] to be edited |
| device         | switch device as text | like 'switch0'                                                   |
| vlan           | number                | number of the vlan (begins at 1)                                 |
| vid            | text                  | custom id of the vlan                                            |
| ports          | array of strings      | ports to be bridged by this switch (like: [0t, 4, 5])            |

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
  switch_vlans: [{
    index: 0,
    device: switch0,
    vlan: 1,
    vid: 1,
    ports: [0, 2, 4, 5]
  }, {
    index: 2,
    device: switch0,
    vlan: 3,
    vid: 10,
    ports: [0t, 3]
  }]
```

[http://wiki.openwrt.org/doc/uci/network]: http://wiki.openwrt.org/doc/uci/network
