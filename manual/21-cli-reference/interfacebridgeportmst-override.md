---
type: Reference
title: "/interface/bridge/port/mst-override"
description: "RouterOS directory reference for /interface/bridge/port/mst-override"
timestamp: '2026-10-06'
status: active
tags: [routeros, mikrotik, manual, cli-reference]
resource: https://manual.mikrotik.com/docs/cli-reference/interface/bridge/port/mst-override.md
sources:
  - resource: https://manual.mikrotik.com/docs/cli-reference/interface/bridge/port/mst-override.md
---

-----------

## interface/bridge/port/mst-override 
**Type:** Directory

<ArgTable c1="Flag" c2="Name" c3="Description">
<ArgTableRow arg="X" typ="disabled">disabled</ArgTableRow>
<ArgTableRow arg="D" typ="dynamic">dynamic</ArgTableRow>
</ArgTable>

<ArgTable c1="Argument" c2="Type" c3="Description">
<ArgTableRow arg="interface" typ="iface_enum" mandatory="1"></ArgTableRow>
<ArgTableRow arg="identifier" typ="num" mandatory="1"></ArgTableRow>
<ArgTableRow arg="priority" typ="enum (0x00 | 0x10 | 0x20 | 0x30 | 0x40 | 0x50 | 0x60 | 0x70 | 0x80 | 0x90 | 0xa0 | 0xb0 | 0xc0 | 0xd0 | 0xe0 | 0xf0) { 0x00:0x00, 0x10:0x10, 0x20:0x20, 0x30:0x30, 0x40:0x40, 0x50:0x50, 0x60:0x60, 0x70:0x70, 0x80:0x80, 0x90:0x90, 0xa0:0xa0, 0xb0:0xb0, 0xc0:0xc0, 0xd0:0xd0, 0xe0:0xe0, 0xf0:0xf0 }"></ArgTableRow>
<ArgTableRow arg="internal-path-cost" typ="num"></ArgTableRow>
</ArgTable>

<ArgTable c1="Read-only Argument" c2="Type" c3="Description">
<ArgTableRow arg="debug-info" typ="string"></ArgTableRow>
</ArgTable>
