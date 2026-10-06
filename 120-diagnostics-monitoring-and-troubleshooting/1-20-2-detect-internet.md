---
type: Reference
title: "Detect Internet"
description: "Detect Internet is a tool that categorizes monitored interfaces into the following states-Internet, WAN, LAN, unknown, slave, and no-link."
timestamp: '2026-05-26'
status: active
tags: [routeros, mikrotik, networking]
resource: ~/Downloads/ROS-260526-1445-796.pdf
sources:
  - resource: https://manual.mikrotik.com/docs/introduction/
---

# Detect Internet

## Introduction

Detect Internet is a tool that categorizes monitored interfaces into the following states-Internet, WAN, LAN, unknown, slave, and no-link.

Note that Detect Internet can install DHCP clients, default routes, DNS servers and affect other facilities. Use with precaution, and after enabling the service, check how it interferes with your other configuration.

State

This submenu displays status of all monitored interfaces defined by the detect-interface-list parameter:

interface/detect-internet/state/print

LAN

All layer 2 interfaces initially have this state.

WAN

Any L3 tunnel and LTE interfaces will initially have this state. Layer 2 interfaces can obtain this state if the following conditions are met:

an interface has an active route to 8.8.8.8 in main routing table. an interface can obtain (dynamic DHCP client is created) or has obtained an address from DHCP (does not apply if DHCP server is also running Detect Internet on the DHCP server interface).

WAN interface can fall back to LAN state only when link status changes. LAN interfaces get locked to LAN after 1h and then change only when link status changes.

Internet

WAN interfaces that can reach cloud.mikrotik.com using UDP protocol port 30000 can obtain this state. Reachability is checked every minute. By default, if a cloud is not reached for 4 minutes, the state falls back to WAN.
