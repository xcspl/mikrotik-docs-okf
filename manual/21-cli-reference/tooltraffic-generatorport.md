---
type: Reference
title: "/tool/traffic-generator/port"
description: "RouterOS directory reference for /tool/traffic-generator/port"
timestamp: '2026-10-06'
status: active
tags: [routeros, mikrotik, manual, cli-reference]
resource: https://manual.mikrotik.com/docs/cli-reference/tool/traffic-generator/port.md
sources:
  - resource: https://manual.mikrotik.com/docs/cli-reference/tool/traffic-generator/port.md
---

-----------

## tool/traffic-generator/port 
**Type:** Directory

<ArgTable c1="Flag" c2="Name" c3="Description">
<ArgTableRow arg="X" typ="disabled">disabled</ArgTableRow>
<ArgTableRow arg="I" typ="invalid">invalid</ArgTableRow>
<ArgTableRow arg="D" typ="dynamic">dynamic</ArgTableRow>
</ArgTable>

<ArgTable c1="Argument" c2="Type" c3="Description">
<ArgTableRow arg="name" typ="string"></ArgTableRow>
<ArgTableRow arg="interface" typ="iface_enum" mandatory="1"></ArgTableRow>
</ArgTable>

<ArgTable c1="Read-only Argument" c2="Type" c3="Description">
<ArgTableRow arg="first-header" typ="enum (mac | vlan | ip | udp | raw | ipv6 | tcp) { mac:1, vlan:2, ip:3, udp:4, raw:5, ipv6:6, tcp:7 }"></ArgTableRow>
</ArgTable>
