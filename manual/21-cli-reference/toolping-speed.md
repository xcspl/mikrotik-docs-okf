---
type: Reference
title: "/tool/ping-speed"
description: "RouterOS command reference for /tool/ping-speed"
timestamp: '2026-10-06'
status: active
tags: [routeros, mikrotik, manual, cli-reference]
resource: https://manual.mikrotik.com/docs/cli-reference/tool/ping-speed.md
sources:
  - resource: https://manual.mikrotik.com/docs/cli-reference/tool/ping-speed.md
---

-----------

## tool/ping-speed 
**Conditions:** !smips
**Type:** Command

<ArgTable c1="Argument" c2="Type" c3="Description">
<ArgTableRow arg="address" typ="ipAddr"></ArgTableRow>
<ArgTableRow arg="first-ping-size" typ="num"></ArgTableRow>
<ArgTableRow arg="second-ping-size" typ="num"></ArgTableRow>
<ArgTableRow arg="time-between-pings" typ="time"></ArgTableRow>
</ArgTable>

<ArgTable c1="Read-only Argument" c2="Type" c3="Description">
<ArgTableRow arg="current" typ="num"></ArgTableRow>
<ArgTableRow arg="average" typ="num"></ArgTableRow>
</ArgTable>
