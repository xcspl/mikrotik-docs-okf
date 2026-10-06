---
type: Reference
title: "/system/console"
description: "RouterOS directory reference for /system/console"
timestamp: '2026-10-06'
status: active
tags: [routeros, mikrotik, manual, cli-reference]
resource: https://manual.mikrotik.com/docs/cli-reference/system/console.md
sources:
  - resource: https://manual.mikrotik.com/docs/cli-reference/system/console.md
---

-----------

## system/console 
**Type:** Directory

<ArgTable c1="Flag" c2="Name" c3="Description">
<ArgTableRow arg="*" typ="default"></ArgTableRow>
<ArgTableRow arg="X" typ="disabled"></ArgTableRow>
<ArgTableRow arg="W" typ="wedged"></ArgTableRow>
<ArgTableRow arg="U" typ="used"></ArgTableRow>
<ArgTableRow arg="F" typ="free"></ArgTableRow>
</ArgTable>

<ArgTable c1="Argument" c2="Type" c3="Description">
<ArgTableRow arg="port" typ="enum"></ArgTableRow>
<ArgTableRow arg="channel" typ="num"></ArgTableRow>
<ArgTableRow arg="term" typ="string"></ArgTableRow>
</ArgTable>

<ArgTable c1="Read-only Argument" c2="Type" c3="Description">
<ArgTableRow arg="vcno" typ="num"></ArgTableRow>
</ArgTable>
