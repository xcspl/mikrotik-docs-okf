---
type: Reference
title: "/lcd/interface"
description: "RouterOS directory reference for /lcd/interface"
timestamp: '2026-10-06'
status: active
tags: [routeros, mikrotik, manual, cli-reference]
resource: https://manual.mikrotik.com/docs/cli-reference/lcd/interface.md
sources:
  - resource: https://manual.mikrotik.com/docs/cli-reference/lcd/interface.md
---

-----------

## lcd/interface 
**Conditions:** !smips
**Syscap:** lcd
**Type:** Directory

<ArgTable c1="Flag" c2="Name" c3="Description">
<ArgTableRow arg="*" typ="default">default</ArgTableRow>
<ArgTableRow arg="I" typ="inactive">inactive</ArgTableRow>
<ArgTableRow arg="X" typ="disabled">disabled</ArgTableRow>
<ArgTableRow arg="D" typ="displayed">displayed</ArgTableRow>
<ArgTableRow arg="W" typ="default-wireless">default-wireless</ArgTableRow>
</ArgTable>

<ArgTable c1="Argument" c2="Type" c3="Description">
<ArgTableRow arg="interface" typ="iface_enum" mandatory="1"></ArgTableRow>
<ArgTableRow arg="timeout" typ="time"></ArgTableRow>
<ArgTableRow arg="max-speed" typ="num" mandatory="1"></ArgTableRow>
</ArgTable>
