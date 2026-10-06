---
type: Reference
title: "/ip/traffic-flow/target"
description: "RouterOS directory reference for /ip/traffic-flow/target"
timestamp: '2026-10-06'
status: active
tags: [routeros, mikrotik, manual, cli-reference]
resource: https://manual.mikrotik.com/docs/cli-reference/ip/traffic-flow/target.md
sources:
  - resource: https://manual.mikrotik.com/docs/cli-reference/ip/traffic-flow/target.md
---

-----------

## ip/traffic-flow/target 
**Type:** Directory

<ArgTable c1="Flag" c2="Name" c3="Description">
<ArgTableRow arg="X" typ="disabled">disabled</ArgTableRow>
</ArgTable>

<ArgTable c1="Argument" c2="Type" c3="Description">
<ArgTableRow arg="src-address" typ="alt { ip: ipAddr
, ipv6: ip6Addr
 }"></ArgTableRow>
<ArgTableRow arg="dst-address" typ="alt { ip: ipAddr
, ipv6: ip6Addr
 }" mandatory="1"></ArgTableRow>
<ArgTableRow arg="port" typ="num"></ArgTableRow>
<ArgTableRow arg="version" typ="enum (1 | 5 | 9 | ipfix) { 1:1, 5:5, 9:9, ipfix:10 }"></ArgTableRow>
<ArgTableRow arg="v9-template-refresh" typ="num"></ArgTableRow>
<ArgTableRow arg="v9-template-timeout" typ="time"></ArgTableRow>
</ArgTable>
