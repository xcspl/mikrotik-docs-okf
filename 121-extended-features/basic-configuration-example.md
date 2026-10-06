---
type: Reference
title: "Basic Configuration Example"
description: "There are multiple ways to configure VETH. Below are simple examples."
timestamp: '2026-05-26'
status: active
tags: [routeros, mikrotik, networking]
resource: ~/Downloads/ROS-260526-1445-796.pdf
sources:
  - resource: https://help.mikrotik.com/docs/spaces/ROS/pages/328059/RouterOS
---

# Basic Configuration Example

There are multiple ways to configure VETH. Below are simple examples.

# VETH with DHCP-client /interface/veth add dhcp=yes

# VETH with static address /interface/veth add address=10.1.1.10/24 gateway=10.1.1.1

After configuring the interface, you can assign it to a container. The container should obtain either the IP assigned by the DHCP server or the static address.

## Properties

VETH

Sub-menu: /interface/veth/add

Configuration settings for the VETH interface.

address (address; Default: None) IPv4 or IPv6 address the interface will be assigned

gateway (IPv4 address; Default: None) IPv4 gateway address

gateway6 (IPv6 address; Default: None) IPv6 gateway address

mac-address (MAC address; Default: None) Interface MAC address

container-mac-address (MAC address; Default: None) MAC address that will be assigned to the container

dhcp (yes / no; Default: no) Enables DHCP client on the interface

name (string; Default: None) Interface name
