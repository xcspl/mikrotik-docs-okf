---
type: Reference
title: "/system/gps/monitor"
description: "RouterOS command reference for /system/gps/monitor"
timestamp: '2026-10-06'
status: active
tags: [routeros, mikrotik, manual, cli-reference]
resource: https://manual.mikrotik.com/docs/cli-reference/system/gps/monitor.md
sources:
  - resource: https://manual.mikrotik.com/docs/cli-reference/system/gps/monitor.md
---

-----------

## system/gps/monitor 
**Package:** gps
**Type:** Command

<ArgTable c1="Read-only Argument" c2="Type" c3="Description">
<ArgTableRow arg="date-and-time" typ="date"></ArgTableRow>
<ArgTableRow arg="latitude" typ="string"></ArgTableRow>
<ArgTableRow arg="longitude" typ="string"></ArgTableRow>
<ArgTableRow arg="altitude" typ="string"></ArgTableRow>
<ArgTableRow arg="speed" typ="string"></ArgTableRow>
<ArgTableRow arg="destination-bearing" typ="string"></ArgTableRow>
<ArgTableRow arg="true-bearing" typ="string"></ArgTableRow>
<ArgTableRow arg="magnetic-bearing" typ="string"></ArgTableRow>
<ArgTableRow arg="valid" typ="bool"></ArgTableRow>
<ArgTableRow arg="satellites" typ="num"></ArgTableRow>
<ArgTableRow arg="fix-quality" typ="num"></ArgTableRow>
<ArgTableRow arg="horizontal-dilution" typ="num"></ArgTableRow>
<ArgTableRow arg="data-age" typ="alt { never: enum (never) { never:0 }
, time: time
 }"></ArgTableRow>
</ArgTable>
