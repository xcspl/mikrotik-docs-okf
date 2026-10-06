---
type: Reference
title: "/disk/blink"
description: "RouterOS command reference for /disk/blink"
timestamp: '2026-10-06'
status: active
tags: [routeros, mikrotik, manual, cli-reference]
resource: https://manual.mikrotik.com/docs/cli-reference/disk/blink.md
sources:
  - resource: https://manual.mikrotik.com/docs/cli-reference/disk/blink.md
---

-----------

## disk/blink 
**Conditions:** !smips
**Type:** Command

<ArgTable c1="Argument" c2="Type" c3="Description">
<ArgTableRow arg="slots" typ="multi { array-id, slot: enum
 }">Disks whose LED should blink, if device supports it.</ArgTableRow>
</ArgTable>
