---
type: Reference
title: "/system/ptp/port"
description: "RouterOS directory reference for /system/ptp/port"
timestamp: '2026-10-06'
status: active
tags: [routeros, mikrotik, manual, cli-reference]
resource: https://manual.mikrotik.com/docs/cli-reference/system/ptp/port.md
sources:
  - resource: https://manual.mikrotik.com/docs/cli-reference/system/ptp/port.md
---

-----------

## system/ptp/port 
**Conditions:** !smips
**Syscap:** ptp
**Type:** Directory

<ArgTable c1="Flag" c2="Name" c3="Description">
<ArgTableRow arg="I" typ="inactive"></ArgTableRow>
<ArgTableRow arg="X" typ="disabled"></ArgTableRow>
</ArgTable>

<ArgTable c1="Argument" c2="Type" c3="Description">
<ArgTableRow arg="ptp" typ="enum" mandatory="1"></ArgTableRow>
<ArgTableRow arg="interface" typ="iface_enum" mandatory="1"></ArgTableRow>
<ArgTableRow arg="role" typ="enum (bmca | master | slave)"></ArgTableRow>
<ArgTableRow arg="announce-interval" typ="num"></ArgTableRow>
<ArgTableRow arg="sync-interval" typ="num"></ArgTableRow>
<ArgTableRow arg="delay-interval" typ="num"></ArgTableRow>
<ArgTableRow arg="pdelay-interval" typ="num"></ArgTableRow>
<ArgTableRow arg="vlan-id" typ="num"></ArgTableRow>
</ArgTable>
