---
type: Reference
title: "PtP GUI example"
description: "This example shows how to configure transparent wireless bridge in GUI from one W60G device to another."
timestamp: '2026-10-06'
status: active
tags: [routeros, mikrotik, networking]
resource: ~/Downloads/ROS-260526-1445-796.pdf
sources:
  - resource: https://manual.mikrotik.com/docs/introduction/
---

# PtP GUI example

Summary

This example shows how to configure transparent wireless bridge in GUI from one W60G device to another.

Example is done from empty configuration state with [WinBox] utility

Connect to the device

After configuration reset-only mac-telnet is possible. In main WinBox screen press on Neighbours, choose your devices MAC address and press Connect:

Configure bridge

Add new bridge and assign bridge members to it. This will allow to pass traffic from from Ethernet to W60G interface without routing.

1. Open Bridge sub-menu;
2. Press on "+" to add new bridge;
3. Apply your changes.

Add interface members (ether1 and wlan60-1) to newly created bridge.

1. Press on Ports sub-menu;
2. Add new member with "+";
3. Select correct interfaces;
4. Apply the settings.

### <u>Set up wireless connection</u>

All previously explained steps are identical to bridge and station devices. Different modes needs to be used when configuring wireless interfaces.

Configure bridge device as follows:

1. Open Interface menu;
2. Double click on wlan60-1 interface;
3. Press on Wireless sub-menu and set mode to bridge;
4. Set SSID and password and region;
5. Select previously created bridge under "Put Stations In Bridge";
6. Apply your changes;
7. Press enable to start transmitting.
Configure station device as follows:

1. Open Interface menu;
2. Double click on wlan60-1 interface;
3. Press on Wireless sub-menu and set mode to station bridge;
4. Set SSID and password;
5. Apply your changes;
6. Press enable to start transmitting.

### <u>Additional configuration</u>

Interfaces when enabled from greyed out will become active.

Link should be established after all previously explained steps are done. It's recommended to set up administrator password on both devices.

To create point to multi-point setup: On bridge device ap-bridge must be set and station-bridge for stations.
