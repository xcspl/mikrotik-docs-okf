---
type: Reference
title: "Feature support based on architecture"
description: "RouterOS manual, section Getting started — Feature support based on architecture."
timestamp: '2026-10-06'
status: active
tags: [routeros, mikrotik, networking]
resource: ~/Downloads/ROS-260526-1445-796.pdf
sources:
  - resource: https://manual.mikrotik.com/docs/introduction/
---

# Feature support based on architecture

All devices support the same features, with a few exceptions, clarified in the below table:

Architecture Not supported Exclusively supported

ARM (ARM32) Zerotier, Container (only ARM32 / ARMv5 containers), BTH

ARM64 Zerotier, Container, BTH

MIPSBE Zerotier, Dude server

MMIPS Zerotier

SMIPS Zerotier, DOT1X, BGP, MPLS, PIMSM, Dude server, User manager

TILE Zerotier BTH

PPC Zerotier, Dude server

X86 PC Zerotier, Cloud Container

CHR VM

Apart from features, there are also a few differences in hardware capabilities, based on the specific model of device. For these differences, please see the below articles:

Wifi-new driver implementation for 802.11ax devices and supported older devices [https://help.mikrotik.com/docs/display/ROS/Wifi](https://help.mikrotik.com/docs/display/ROS/Wifi) L3 Hardware offloading [https://help.mikrotik.com/docs/display/ROS/L3+Hardware+Offloading#L3HardwareOffloading-L3HWDeviceSupport](https://help.mikrotik.com/docs/display/ROS/L3+Hardware+Offloading#L3HardwareOffloading-L3HWDeviceSupport) PTP [https://help.mikrotik.com/docs/display/ROS/Precision+Time+Protocol](https://help.mikrotik.com/docs/display/ROS/Precision+Time+Protocol) Switch chip features [https://help.mikrotik.com/docs/display/ROS/Switch+Chip+Features](https://help.mikrotik.com/docs/display/ROS/Switch+Chip+Features)
