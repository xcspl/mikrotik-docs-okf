---
type: Reference
title: "Configuration"
description: "RouterOS manual, section Diagnostics, monitoring and troubleshooting — Configuration."
timestamp: '2026-05-26'
status: active
tags: [routeros, mikrotik, networking]
resource: ~/Downloads/ROS-260526-1445-796.pdf
sources:
  - resource: https://manual.mikrotik.com/docs/introduction/
---

# Configuration

/interface detect-internet

Property Description

detect-interface-list (interface list; Default: none) All interfaces in the list will be monitored by Detect Internet

internet-interface-list (interface list; Default: none) Interfaces with state Internet will be dynamically added to this list

lan-interface-list (interface list; Default: none) Interfaces with state Lan will be dynamically added to this list

wan-interface-list (interface list; Default: none) Interfaces with state Wan will be dynamically added to this list

request-interval (time; Default: 2m) Time interval between checks of interface status

[admin@MikroTik] > interface/detect-internet/print detect-interface-list: none lan-interface-list: none wan-interface-list: none internet-interface-list: none [admin@MikroTik] > interface/detect-internet/set internet-interface-list=all wan-interface-list=all lan- interface-list=all detect-interface-list=all [admin@MikroTik] > interface/detect-internet/state/print Columns: NAME, STATE, STATE-CHANGE-TIME, CLOUD-RTT # NAME STATE STATE-CHANGE-TIME CLO 0 ether1 internet dec/22/2020 13:46:18 5ms
