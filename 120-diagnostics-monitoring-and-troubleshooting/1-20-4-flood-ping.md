---
type: Reference
title: "Flood Ping"
description: "RouterOS manual, section 1.20.4 — Flood Ping."
timestamp: '2026-10-06'
status: active
tags: [routeros, mikrotik, networking]
resource: ~/Downloads/ROS-260526-1445-796.pdf
sources:
  - resource: https://manual.mikrotik.com/docs/introduction/
---

# Flood Ping

Summary Quick Example

## Summary

Flood Ping tool allows to generate a burst of ICMP packets towards specific host and provides simple statistics about the results

## Quick Example

In the following example, we will send 1000 ping packets towards specific IP address:

[admin@MikroTik] > /tool/flood-ping address=10.155.114.1 count=1000 sent: 1000 received: 1000 min-rtt: 0 avg-rtt: 0 max-rtt: 1

[admin@MikroTik] > /tool/flood-ping address=2001:0db8::2 sent: 500 received: 500 min-rtt: 0 avg-rtt: 0 max-rtt: 3
