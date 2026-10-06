---
type: Reference
title: "/interface/mesh/traceroute"
description: "RouterOS command reference for /interface/mesh/traceroute"
timestamp: '2026-10-06'
status: active
tags: [routeros, mikrotik, manual, cli-reference]
resource: https://manual.mikrotik.com/docs/cli-reference/interface/mesh/traceroute.md
sources:
  - resource: https://manual.mikrotik.com/docs/cli-reference/interface/mesh/traceroute.md
---

-----------

## interface/mesh/traceroute 
**Type:** Command

<ArgTable c1="Argument" c2="Type" c3="Description">
<ArgTableRow arg="mesh" typ="iface_enum"></ArgTableRow>
<ArgTableRow arg="address" typ="macAddr"></ArgTableRow>
<ArgTableRow arg="hoplimit" typ="num"></ArgTableRow>
</ArgTable>

<ArgTable c1="Read-only Argument" c2="Type" c3="Description">
<ArgTableRow arg="address" typ="macAddr"></ArgTableRow>
<ArgTableRow arg="time" typ="num"></ArgTableRow>
<ArgTableRow arg="status" typ="enum (success | ttl-exceeded | no-route | timeout) { success:1, ttl-exceeded:2, no-route:3, timeout:4 }"></ArgTableRow>
</ArgTable>
