---
layout: post
title: Cisco Asa Firewall DHCP Configuration
subtitle: Static IP to Mac address mapping
bigimg: /img/kelly-sikkema-PMxoh8zJNb0-unsplash.png
tags: [devops]
---

Adding static IP to Mac address mapping to your firewalls dhcpd configuration is now supported on ASA version 9.13(1) and later.

You need to do the configuration on the command line since it is not yet available in the ASDM gui:


``` text
config t

dhcpd reserve-address 192.168.1.6 aaaa.bbbb.cccc INSIDE
...

wr mem
```

It works great, I just needed to upgrade the firmware for ASA and ASDM.


Best,
Mark


## Resources
* [ASA 5505 DHCP Reservation list](https://community.cisco.com/t5/network-security/asa-5505-dhcp-reservation-list/m-p/4033184/highlight/true#M1049625)

