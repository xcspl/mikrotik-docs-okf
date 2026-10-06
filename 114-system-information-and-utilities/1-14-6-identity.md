---
type: Reference
title: "Identity"
description: "RouterOS manual, section 1.14.6 — Identity."
timestamp: '2026-05-26'
status: active
tags: [routeros, mikrotik, networking]
resource: ~/Downloads/ROS-260526-1445-796.pdf
sources:
  - resource: https://manual.mikrotik.com/docs/introduction/
---

# Identity

## Overview

Setting the System's Identity provides a unique identifying name for when the system identifies itself to other routers in the network and when accessing services such as DHCP, Neighbour Discovery, and default wireless SSID. The default system Identity is set to 'MikroTik'.

System Identity has a 64 maximum character length

## Configuration

To set system identity in RouterOS:

[admin@MikroTik] > /system identity set name=New_Identity [admin@New_Identity] >

The current System Identity is always displayed after the logged-in account name and with the print command:

[admin@New_Identity] /system identity>print name: New_Identity [admin@New_Identity] /system identity>

SNMP

It is also possible to change the router system identity by SNMP set command:

snmpset -c public -v 1 192.168.0.0 1.3.6.1.2.1.1.5.0 s New_Identity

snmpset-Linux based SNMP application used for SNMP SET requests to set information on a network entity;

public-router's community name;

192.168.0.0 - IP address of the router;
1.3.6.1.2.1.1.5.0 - SNMP value for router's identity;
