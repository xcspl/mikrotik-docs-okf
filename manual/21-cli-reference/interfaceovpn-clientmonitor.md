---
type: Reference
title: "/interface/ovpn-client/monitor"
description: "RouterOS command reference for /interface/ovpn-client/monitor"
timestamp: '2026-10-06'
status: active
tags: [routeros, mikrotik, manual, cli-reference]
resource: https://manual.mikrotik.com/docs/cli-reference/interface/ovpn-client/monitor.md
sources:
  - resource: https://manual.mikrotik.com/docs/cli-reference/interface/ovpn-client/monitor.md
---

-----------

## interface/ovpn-client/monitor 
**Type:** Command

<ArgTable c1="Read-only Argument" c2="Type" c3="Description">
<ArgTableRow arg="status" typ="string">Current connection status.</ArgTableRow>
<ArgTableRow arg="uptime" typ="time">Connection uptime.</ArgTableRow>
<ArgTableRow arg="encoding" typ="string">Encryption encoding used.</ArgTableRow>
<ArgTableRow arg="mtu" typ="num">Current MTU of the connection.</ArgTableRow>
<ArgTableRow arg="local-address" typ="ipAddr">Local IP address of the connection.</ArgTableRow>
<ArgTableRow arg="remote-address" typ="ipAddr">Remote IP address of the connection.</ArgTableRow>
</ArgTable>
