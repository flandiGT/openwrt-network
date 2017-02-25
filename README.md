openwrt-network
===============

configure network aspects of your openwrt system.

Dependencies
------------

* [openwrt-uci](https://github.com/flandiGT/openwrt-uci)


Role Variables
--------------

| variable name     | type                   | default  | available options and examples             |
|-------------------|------------------------|----------|--------------------------------------------|
| interfaces        | dict with objects      | {}       | key = interface name                       |
| switch_vlans      | array with objects     | <empty>  | see attributes in object description below |

interface structure:

| variable name     | type                   | available options and examples       |
|-------------------|------------------------|--------------------------------------|
| proto             | option as text         | (see official documentation)         |
| ifname            | text                   | covered interface (like eth0)        |
| ipaddr            | text                   | IP address (for static proto)        |
| netmask           | text                   | IP netmask (for static proto)        |
| username          | text                   | username for PPPoE                   |
| password          | text                   | password for PPPoE                   |

switch_vlans attributes:

| attribute name | property type         | valid values / examples                                          |
|----------------|-----------------------|------------------------------------------------------------------|
| index          | array_index as number | specify the element index in network.switch_vlans[] to be edited |
| device         | switch device as text | like 'switch0'                                                   |
| vlan           | number                | number of the vlan (begins at 1)                                 |
| vid            | text                  | custom id of the vlan                                            |
| ports          | array of strings      | ports to be bridged by this switch (like: [0t, 4, 5])            |

Example Playbook
----------------

```
- role: openwrt-network
  interfaces:
    wan:
      proto: pppoe
      username: my_username
      password: my_password
    vpn:
      ifname: tun0
      proto: none
      auto: True
    guest:
      ifname: eth0
      proto: static
      ipaddr: 10.0.0.1
      netmask: 255.255.255.0
  switch_vlans:
    - index: 0
      device: switch0
      vlan: 1
      vid: 1
      ports:
        - 0
        - 2
        - 4
        - 5
    - index: 2
      device: switch0
      vlan: 3
      vid: 10
      ports:
        - 0t
        - 3
```

Official documentation:
* [OpenWRT Wiki / Network configuration](http://wiki.openwrt.org/doc/uci/network)
