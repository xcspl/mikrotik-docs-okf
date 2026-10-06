---
type: Reference
title: "/system/console/screen"
description: "RouterOS settings reference for /system/console/screen"
timestamp: '2026-10-06'
status: active
tags: [routeros, mikrotik, manual, cli-reference]
resource: https://manual.mikrotik.com/docs/cli-reference/system/console/screen.md
sources:
  - resource: https://manual.mikrotik.com/docs/cli-reference/system/console/screen.md
---

-----------

## system/console/screen 
**Conditions:** i386
**Type:** Settings Directory

<ArgTable c1="Argument" c2="Type" c3="Description">
<ArgTableRow arg="line-count" typ="enum (25 | 40 | 50) { 25:2, 40:1, 50:0 }"></ArgTableRow>
<ArgTableRow arg="blank-interval" typ="enum (never | 1min | 10min | 60min) { never:0, 1min:1, 10min:10, 60min:60 }"></ArgTableRow>
</ArgTable>
