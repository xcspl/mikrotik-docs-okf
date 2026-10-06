---
type: Reference
title: "<u>Packet flow</u>"
description: "b. For a multi-destination packet (broadcast, multicast or unknown-unicast), the PE will send a single packet replica per every extended port (except for the source port where the packet was received)."
timestamp: '2026-10-06'
status: active
tags: [routeros, mikrotik, networking]
resource: ~/Downloads/ROS-260526-1445-796.pdf
sources:
  - resource: https://manual.mikrotik.com/docs/introduction/
---

# <u>Packet flow</u>

To better understand the underlying principles of Controlling Bridge and Port Extender, a packet walkthrough is provided below:

1. An L2 packet is received on the extended port;
2. The Port Extender encapsulates the packet with an E-TAG header (EtherType 0x893F) and forwards it through an upstream port, towards the Controller Bridge. An E-TAG packet contains information regarding the PE source port ID. The PE device does not make any local switching decisions;
3. The Controller Bridge receives the E-TAG packet and knows exactly which extended interface received it. The CB then internally decapsulates the packet and proceed it through a regular switching decision (host learning, destination address lookup, VLAN filtering, etc.);
4. Once a switching decision is made, the CB will again encapsulate the original packet with an E-TAG and send it through a cascade port, towards Port Extender;
a. For a single destination packet (unicast), the CB will include the PE destination port ID in the E-TAG and send it through a correct cascade port;
b. For a multi-destination packet (broadcast, multicast or unknown-unicast), the CB will include a target group mark and source port ID in the E-TAG and send a single packet replica per every cascade port;
5. Once a PE device receives an E-TAG packet on the upstream port, PE decapsulates it and sends the original L2 packet through the extended port;
a. For a single destination packet (unicast), the PE will send the packet only to the correct extended port;
b. For a multi-destination packet (broadcast, multicast or unknown-unicast), the PE will send a single packet replica per every extended port (except for the source port where the packet was received).
