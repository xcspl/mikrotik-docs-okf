---
type: Reference
title: "Group Management Protocol"
description: "The Group Management Protocol allows any of the interfaces to become a receiver for the multicast stream. It allows testing the multicast routing and switching setups without using dedicated IGMP or MLD clients. The opti."
timestamp: '2026-05-26'
status: active
tags: [routeros, mikrotik, networking]
resource: ~/Downloads/ROS-260526-1445-796.pdf
sources:
  - resource: https://manual.mikrotik.com/docs/introduction/
---

# Group Management Protocol

Introduction Examples

## <u>Introduction</u>

The Group Management Protocol allows any of the interfaces to become a receiver for the multicast stream. It allows testing the multicast routing and switching setups without using dedicated IGMP or MLD clients. The option is available since RouterOS v7.4 and it supports IGMP v1, v2, v3 and MLD v1, v2 protocols.

Interfaces are using IGMP v3 and MLD v2 by default. In case IGMP v1, v2 or MLD v1 queries are received, the interfaces will fall back to the appropriate version. Once Group Management Protocol is created on the interface, it will send an unsolicited membership report (join) packet and respond to query messages. If the configuration is removed or disabled, the interface will send a leave message.

## <u>Examples</u>

This example shows how to configure a simple multicast listener on the interface.

First, add an IP address on the interface:

/ip address add address=192.168.10.10/24 interface=ether1 network=192.168.10.0

Then configure Group Management Protocol on the same interface:

/routing gmp add groups=229.1.1.1 interfaces=ether1

It is now possible to check your multicast network to see if routers or switches have created the appropriate multicast forwarding entries and whether multicast data is being received on the interface (see the interface stats, or use a Packet Sniffer and Torch).
