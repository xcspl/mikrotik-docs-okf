---
type: Reference
title: "/interface/wifi/aaa"
description: "RouterOS directory reference for /interface/wifi/aaa"
timestamp: '2026-10-06'
status: active
tags: [routeros, mikrotik, manual, cli-reference]
resource: https://manual.mikrotik.com/docs/cli-reference/interface/wifi/aaa.md
sources:
  - resource: https://manual.mikrotik.com/docs/cli-reference/interface/wifi/aaa.md
---

-----------

## interface/wifi/aaa 
**Type:** Directory

<ArgTable c1="Flag" c2="Name" c3="Description">
<ArgTableRow arg="X" typ="disabled">disabled</ArgTableRow>
</ArgTable>

<ArgTable c1="Argument" c2="Type" c3="Description">
<ArgTableRow arg="name" typ="string" mandatory="1"></ArgTableRow>
<ArgTableRow arg="username-format" typ="string" unset="1"></ArgTableRow>
<ArgTableRow arg="password-format" typ="string" unset="1"></ArgTableRow>
<ArgTableRow arg="called-format" typ="string" unset="1"></ArgTableRow>
<ArgTableRow arg="calling-format" typ="string" unset="1"></ArgTableRow>
<ArgTableRow arg="mac-caching" typ="alt { mac-caching-disable: enum (disabled) { disabled:0 }
, mac-caching-time: time
 }" unset="1"></ArgTableRow>
<ArgTableRow arg="interim-update" typ="alt { interim-update-disable: enum (disabled) { disabled:0 }
, interim-update-time: time [1 .. ]
 }" unset="1"></ArgTableRow>
<ArgTableRow arg="nas-identifier" typ="string" unset="1"></ArgTableRow>
</ArgTable>
