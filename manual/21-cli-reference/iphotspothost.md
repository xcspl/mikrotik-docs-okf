---
type: Reference
title: "/ip/hotspot/host"
description: "RouterOS directory reference for /ip/hotspot/host"
timestamp: '2026-10-06'
status: active
tags: [routeros, mikrotik, manual, cli-reference]
resource: https://manual.mikrotik.com/docs/cli-reference/ip/hotspot/host.md
sources:
  - resource: https://manual.mikrotik.com/docs/cli-reference/ip/hotspot/host.md
---

-----------

## ip/hotspot/host 
**Type:** Directory

<ArgTable c1="Flag" c2="Name" c3="Description">
<ArgTableRow arg="S" typ="static">static</ArgTableRow>
<ArgTableRow arg="H" typ="DHCP">DHCP</ArgTableRow>
<ArgTableRow arg="D" typ="dynamic">dynamic</ArgTableRow>
<ArgTableRow arg="A" typ="authorized">authorized</ArgTableRow>
<ArgTableRow arg="P" typ="bypassed">bypassed</ArgTableRow>
</ArgTable>

<ArgTable c1="Read-only Argument" c2="Type" c3="Description">
<ArgTableRow arg="mac-address" typ="macAddr"></ArgTableRow>
<ArgTableRow arg="address" typ="ipAddr"></ArgTableRow>
<ArgTableRow arg="to-address" typ="ipAddr"></ArgTableRow>
<ArgTableRow arg="server" typ="enum"></ArgTableRow>
<ArgTableRow arg="uptime" typ="time"></ArgTableRow>
<ArgTableRow arg="idle-time" typ="time"></ArgTableRow>
<ArgTableRow arg="idle-timeout" typ="time"></ArgTableRow>
<ArgTableRow arg="keepalive-timeout" typ="time"></ArgTableRow>
<ArgTableRow arg="host-dead-time" typ="time"></ArgTableRow>
<ArgTableRow arg="bridge-port" typ="iface_enum"></ArgTableRow>
<ArgTableRow arg="vlan-id" typ="num"></ArgTableRow>
<ArgTableRow arg="http-proxy" typ="composite { address: ipAddr
, port: num
 }"></ArgTableRow>
<ArgTableRow arg="bytes-in" typ="num"></ArgTableRow>
<ArgTableRow arg="bytes-out" typ="num"></ArgTableRow>
<ArgTableRow arg="packets-in" typ="num"></ArgTableRow>
<ArgTableRow arg="packets-out" typ="num"></ArgTableRow>
<ArgTableRow arg="found-by" typ="string"></ArgTableRow>
</ArgTable>
