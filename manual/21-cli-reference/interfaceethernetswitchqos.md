---
type: Reference
title: "/interface/ethernet/switch/qos"
description: "The entire QoS hardware configuration is located under /in/eth/sw/qos. This centralized approach allows you to store all QoS-related configuration items in one place, making it easy to monitor and export settings"
timestamp: '2026-10-06'
status: active
tags: [routeros, mikrotik, manual, cli-reference]
resource: https://manual.mikrotik.com/docs/cli-reference/interface/ethernet/switch/qos.md
sources:
  - resource: https://manual.mikrotik.com/docs/cli-reference/interface/ethernet/switch/qos.md
---

-----------

## interface/ethernet/switch/qos 
**Syscap:** rbswitch and crs_prestera
**Type:** Directory

The entire QoS hardware configuration is located under `/in/eth/sw/qos`. This centralized approach allows you to store all QoS-related configuration items in one place, making it easy to monitor and export settings using `/in/eth/sw/qos/export`.

QoS entries have two major flag indicators:

- **H** - Hardware-offloaded entry.
- **I** - Inactive entry.
