---
type: Reference
title: "Wake on LAN"
description: "The Wake on LAN tool can send a UDP Magic Packet to the Broadcast address with a selected MAC address embedded in it."
timestamp: '2026-05-26'
status: active
tags: [routeros, mikrotik, networking]
resource: ~/Downloads/ROS-260526-1445-796.pdf
sources:
  - resource: https://help.mikrotik.com/docs/spaces/ROS/pages/328059/RouterOS
---

# Wake on LAN

## Introduction

Sub-menu: /tool wol

The Wake on LAN tool can send a UDP Magic Packet to the Broadcast address with a selected MAC address embedded in it.

If the target device supports Wake on LAN (a target computer has specific hardware and software requirements for the Wake on LAN feature to work), it should wake up from sleep or shutdown state.

Currently, secure WoL is not supported.

## Property Description

Property Description

interface (string; Default: ) Interface through which the Magic Packet will be sent

mac (MAC; Default: ) MAC address of a target computer

## Application Example

The command requires a MAC address parameter and interface.

If an interface is not specified, A Magic Packet will be sent as an IP broadcast from a default gateway interface.

/tool wol mac=FE:4B:71:05:EA:8B interface=ether1
