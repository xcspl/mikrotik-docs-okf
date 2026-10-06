---
type: Reference
title: "MACVLAN"
description: "A MACVLAN interface can only receive broadcast packets, packets addressed to its own MAC address, and a limited number of multicast addresses. If the physical interface has a VLAN configured, the MACVLAN interface cannot."
timestamp: '2026-05-26'
status: active
tags: [routeros, mikrotik, networking]
resource: ~/Downloads/ROS-260526-1445-796.pdf
sources:
  - resource: https://help.mikrotik.com/docs/spaces/ROS/pages/328059/RouterOS
---

# MACVLAN

Overview Basic Configuration Example Property Reference

## Overview

The MACVLAN provides a means to create multiple virtual network interfaces, each with its own unique Media Access Control (MAC) address, attached to a physical network interface. This technology is utilized to address specific network requirements, such as obtaining multiple IP addresses or establishing distinct PPPoE client connections from a single physical Ethernet interface while using different MAC addresses. Unlike traditional VLAN (Virtual LAN) interfaces, which rely on Ethernet frames tagged with VLAN identifiers, MACVLAN operates at the MAC address level, making it a versatile and efficient solution for specific networking scenarios.

A MACVLAN interface can only receive broadcast packets, packets addressed to its own MAC address, and a limited number of multicast addresses. If the physical interface has a VLAN configured, the MACVLAN interface cannot receive packets from that VLAN.

For bridging and more complex Layer2 solutions involving VLANs, a dedicated switch should be used instead.

## Basic Configuration Example

Picture a scenario where the ether1 interface connects to your ISP, and your router needs to lease two IP addresses, each with a distinct MAC address. Traditionally, this would require the use of two physical Ethernet interfaces and an additional switch. However, a more efficient solution is to create a virtual MACVLAN interface.

To create a MACVLAN interface, select the needed Ethernet interface. A MAC address will be automatically assigned if not manually specified:

/interface macvlan add interface=ether1 name=macvlan1

/interface macvlan print Flags: R-RUNNING Columns: NAME, MTU, INTERFACE, MAC-ADDRESS, MODE # NAME MTU INTERFACE MAC-ADDRESS MODE 0 R macvlan1 1500 ether1 76:81:BF:68:69:83 bridge

Now, a DHCP client can be created on ether1 and macvlan1 interfaces:

/ip dhcp-client add interface=ether1 add interface=macvlan1

## Property Reference

Sub-menu: /interface/macvlan

Configuration settings for the MACVLAN interface.

Property Description

arp (disabled | enabled | local-proxy-arp | proxy-arp | reply-only; Default: enabled)

arp-timeout (auto | integer; Default: auto)

comment (string; Default: )

disabled (yes | no; Default: no)

interface (name; Default: )

loop-protect (on | off | default; Default: default)

loop-protect-disable-time (ti me interval | 0; Default: 5m)

loop-protect-send-interval (ti me interval; Default: 5s)

mac-address (MAC; Default: )

mode (private | bridge; Default: bridge)

mtu (integer; Default: 1500)

name (string; Default: )

Address Resolution Protocol setting

disabled-the interface will not use ARP enabled-the interface will use ARP local-proxy-arp -the router performs proxy ARP on the interface and sends replies to the same interface proxy-arp-the router performs proxy ARP on the interface and sends replies to other interfaces reply-only-the interface will only reply to requests originating from matching IP address/MAC address combinations, which are entered as static entries in the IP/ARP table. No dynamic entries will be automatically stored in the IP/ARP table. Therefore, for communications to be successful, a valid static entry must already exist.

Sets for how long the ARP record is kept in the ARP table after no packets are received from IP. Value auto equals to the value of arp-timeout in /ip/settings/, default is 30s.

Short description of the interface.

Changes whether the interface is disabled.

The name of the underlying interface on which the MACVLAN will operate. MACVLAN interfaces can be created on any interface that has a MAC address.

Adding a VLAN interface on top of a MACVLAN interface is not supported. Adding MACVLAN on interface which is already bridged or bonded is not supported.

Enables or disables loop protect on the interface, the default works as turned off.

Sets how long the selected interface is disabled when a loop is detected. 0 - forever.

Sets how often loop protect packets are sent on the selected interface.

Static MAC address of the interface. A randomly generated MAC address will be assigned when not specified.

Sets MACVLAN interface mode:

private-does not allow communication between MACVLAN instances on the same parent interface. bridge-allows communication between MACVLAN instances on the same parent interface.

Sets Layer 3 Maximum Transmission Unit. For the MACVLAN interface, it cannot be higher than the parent interface.

Interface name.
