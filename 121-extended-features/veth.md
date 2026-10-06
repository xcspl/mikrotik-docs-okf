---
type: Reference
title: "VETH"
description: "VETH (Virtual Ethernet) is a special type of virtual network interface primarily used to provide network connectivity for containers. It acts as a virtual Ethernet port that connects RouterOS to a container, allowing the."
timestamp: '2026-05-26'
status: active
tags: [routeros, mikrotik, networking]
resource: ~/Downloads/ROS-260526-1445-796.pdf
sources:
  - resource: https://manual.mikrotik.com/docs/introduction/
---

# VETH

Overview Basic Configuration Example Properties VETH

## Overview

VETH (Virtual Ethernet) is a special type of virtual network interface primarily used to provide network connectivity for containers. It acts as a virtual Ethernet port that connects RouterOS to a container, allowing the container to communicate with other interfaces and networks.

VETH interfaces behave like standard Ethernet interfaces — they can be assigned static IPv4 and IPv6 addresses, obtain addresses via DHCP client. VETH interfaces also support SLAAC. They can also participate in bridges or routing configurations, just like physical interfaces.
