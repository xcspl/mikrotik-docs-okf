---
type: Reference
title: "/interface/mesh/fdb"
description: "RouterOS directory reference for /interface/mesh/fdb"
timestamp: '2026-10-06'
status: active
tags: [routeros, mikrotik, manual, cli-reference]
resource: https://manual.mikrotik.com/docs/cli-reference/interface/mesh/fdb.md
sources:
  - resource: https://manual.mikrotik.com/docs/cli-reference/interface/mesh/fdb.md
---

-----------

## interface/mesh/fdb 
**Type:** Directory

<ArgTable c1="Flag" c2="Name" c3="Description">
<ArgTableRow arg="A" typ="active">active</ArgTableRow>
<ArgTableRow arg="R" typ="root">root</ArgTableRow>
</ArgTable>

<ArgTable c1="Read-only Argument" c2="Type" c3="Description">
<ArgTableRow arg="mesh" typ="iface_enum"></ArgTableRow>
<ArgTableRow arg="type" typ="enum (local | outsider | direct | mesh | neighbor | larval | unknown) { local:1, outsider:2, direct:3, mesh:4, neighbor:5, larval:6, unknown:7 }"></ArgTableRow>
<ArgTableRow arg="mac-address" typ="macAddr"></ArgTableRow>
<ArgTableRow arg="on-interface" typ="iface_enum"></ArgTableRow>
<ArgTableRow arg="lifetime" typ="time"></ArgTableRow>
<ArgTableRow arg="age" typ="time"></ArgTableRow>
<ArgTableRow arg="metric" typ="num"></ArgTableRow>
<ArgTableRow arg="seq-number" typ="num"></ArgTableRow>
</ArgTable>
