---
type: Reference
title: "Fail-over PtP GUI example"
description: "Later in the instructions it requires to assign bridge members to it. This will allow to pass traffic from Ethernet to W60G interface without routing."
timestamp: '2026-05-26'
status: active
tags: [routeros, mikrotik, networking]
resource: ~/Downloads/ROS-260526-1445-796.pdf
sources:
  - resource: https://help.mikrotik.com/docs/spaces/ROS/pages/328059/RouterOS
---

# Fail-over PtP GUI example

Summary

This example shows how to configure automatic fail-over (bonding) 5Ghz link in combination with 60Ghz devices in GUI. When a connection between 60Ghz wireless is lost, it will automatically use the bonded interface. Example is done from empty configuration state with [WinBox] utility

Connect to the device

After configuration reset-only mac-telnet is possible. In main WinBox screen press on Neighbours, choose your devices MAC address and press Connect:

1. Select correct device MAC Address;
2. Login by default is "admin" and no password is set;
3. Press Connect.
Configure bridge

Add new bridge.

1. Open Bridge sub-menu;
2. Press on "+" to add new bridge;
3. Apply your changes.

Later in the instructions it requires to assign bridge members to it. This will allow to pass traffic from Ethernet to W60G interface without routing.

### <u>Set up 60Ghz wireless connection</u>

All previously explained steps are identical to bridge and station devices. Different modes needs to be used when configuring wireless interfaces.

Configure bridge device as follows:

1. Open Interface menu;
2. Double click on wlan60-1 interface;
3. Press on Wireless sub-menu and set mode to bridge (or ap-bridge for PtmP);
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

### <u>Set up 5Ghz wireless connection</u>

Choose Security Profile for your devices -

1. Choose Wireless menu
2. Choose Security Profiles sub-menu
3. Add new profile with "+" sign
4. Choose name, mode, authentication type and a secure password.
5. Apply the configuration.

For bridge device -

1. Open Interfaces menu;
2. Double click on wlan1 interface;
3. Press on Wireless sub-menu and set mode to bridge (or ap-bridge for PtmP);
4. Set SSID, password and country.
5. Press on Advanced Mode.

1. Choose your Security Profile;
2. Apply your changes;
3. Press enable to start transmitting.

For station device -

1. Open Interfaces menu;
2. Double click on wlan1 interface;
3. Press on Wireless sub-menu and set mode to station-bridge;
4. Set SSID, password and country;
5. Press on advanced mode ( similar to bridge device* );
6. Choose Security Profile;
7. Apply your changes;
8. Press enable to start transmitting.

If everything is done correctly-running (R) flags should appear as shown in the screenshot -

### <u>Configure bonding</u>

Configure bonding and assign slave interfaces in this setup it is selected as built in wlan1 interface, but it can be also ether interface in other kind of setups.

For bridge device -

1. Press on Bonding sub-menu;
2.  Add new member with "+";
3. Add interface members (wlan1 and wlan60-station-1) to bonding interface as Slaves;
4. Add interface member wlan60-station-1 as Primary interface;
5. Choose Mode as active backup;
6. Apply configuration.

For station device -

1. Press on Bonding sub-menu;
2.  Add new member with "+";
3. Add interface members (wlan1 and wlan60-1) to bonding interface as Slaves;
4. Add interface member wlan60-1 as Primary interface;
5. Choose Mode as active backup;
6. Apply configuration.

### <u>Configure bridge</u>

Configuring bridge settings including the bonding interface is mandatory for the active-backup to work on used devices ( In this case bridge and station devices settings are the same ).

1. Press on Bridge sub-menu;
2. Add new member with "+";
3. Add interface member as ether1 and Bridge member as bridge1;
4. Apply configuration.

1. Press on Bridge sub-menu;
2. Add new member with "+";
3. Add interface member as bonding1 and Bridge member as bridge1;
4. Apply configuration.

### <u>Additional configuration</u>

Interfaces when enabled from greyed out will become active.

Link should be established after all previously explained steps are done. It's recommended to set up administrator password on both devices.
