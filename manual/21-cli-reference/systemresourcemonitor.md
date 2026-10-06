---
type: Reference
title: "/system/resource/monitor"
description: "RouterOS command reference for /system/resource/monitor"
timestamp: '2026-10-06'
status: active
tags: [routeros, mikrotik, manual, cli-reference]
resource: https://manual.mikrotik.com/docs/cli-reference/system/resource/monitor.md
sources:
  - resource: https://manual.mikrotik.com/docs/cli-reference/system/resource/monitor.md
---

-----------

## system/resource/monitor 
**Type:** Command

<ArgTable c1="Read-only Argument" c2="Type" c3="Description">
<ArgTableRow arg="cpu-used" typ="num"></ArgTableRow>
<ArgTableRow arg="cpu-used-per-core" typ="multi { cpu-used: num
 }" syscap="smp"></ArgTableRow>
<ArgTableRow arg="free-memory" typ="num"></ArgTableRow>
</ArgTable>
