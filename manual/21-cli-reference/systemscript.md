---
type: Reference
title: "/system/script"
description: "RouterOS directory reference for /system/script"
timestamp: '2026-10-06'
status: active
tags: [routeros, mikrotik, manual, cli-reference]
resource: https://manual.mikrotik.com/docs/cli-reference/system/script.md
sources:
  - resource: https://manual.mikrotik.com/docs/cli-reference/system/script.md
---

-----------

## system/script 
**Type:** Directory

<ArgTable c1="Flag" c2="Name" c3="Description">
<ArgTableRow arg="I" typ="invalid"></ArgTableRow>
</ArgTable>

<ArgTable c1="Argument" c2="Type" c3="Description">
<ArgTableRow arg="name" typ="string"></ArgTableRow>
<ArgTableRow arg="owner" typ="string"></ArgTableRow>
<ArgTableRow arg="policy" typ="multi { array-id, policy: enum
 }"></ArgTableRow>
<ArgTableRow arg="dont-require-permissions" typ="bool"></ArgTableRow>
<ArgTableRow arg="source" typ="string"></ArgTableRow>
</ArgTable>

<ArgTable c1="Read-only Argument" c2="Type" c3="Description">
<ArgTableRow arg="last-started" typ="date"></ArgTableRow>
<ArgTableRow arg="run-count" typ="num"></ArgTableRow>
</ArgTable>
