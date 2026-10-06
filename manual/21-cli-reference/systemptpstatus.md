---
type: Reference
title: "/system/ptp/status"
description: "RouterOS directory reference for /system/ptp/status"
timestamp: '2026-10-06'
status: active
tags: [routeros, mikrotik, manual, cli-reference]
resource: https://manual.mikrotik.com/docs/cli-reference/system/ptp/status.md
sources:
  - resource: https://manual.mikrotik.com/docs/cli-reference/system/ptp/status.md
---

-----------

## system/ptp/status 
**Conditions:** !smips
**Syscap:** ptp
**Type:** Directory

<ArgTable c1="Read-only Argument" c2="Type" c3="Description">
<ArgTableRow arg="interface" typ="iface_enum"></ArgTableRow>
<ArgTableRow arg="state" typ="string"></ArgTableRow>
<ArgTableRow arg="delay" typ="num"></ArgTableRow>
<ArgTableRow arg="port-nr" typ="num"></ArgTableRow>
<ArgTableRow arg="as-capable" typ="bool"></ArgTableRow>
<ArgTableRow arg="neigh-freq-drift" typ="num"></ArgTableRow>
</ArgTable>
