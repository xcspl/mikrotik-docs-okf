---
type: Reference
title: "/ipv6/nd/prefix/default"
description: "RouterOS settings reference for /ipv6/nd/prefix/default"
timestamp: '2026-10-06'
status: active
tags: [routeros, mikrotik, manual, cli-reference]
resource: https://manual.mikrotik.com/docs/cli-reference/ipv6/nd/prefix/default.md
sources:
  - resource: https://manual.mikrotik.com/docs/cli-reference/ipv6/nd/prefix/default.md
---

-----------

## ipv6/nd/prefix/default 
**Type:** Settings Directory

<ArgTable c1="Argument" c2="Type" c3="Description">
<ArgTableRow arg="autonomous" typ="bool"></ArgTableRow>
<ArgTableRow arg="dhcp6-pd-preferred" typ="bool"></ArgTableRow>
<ArgTableRow arg="valid-lifetime" typ="alt { special: enum (infinity) { infinity:0xffffffff }
, value: time
 }"></ArgTableRow>
<ArgTableRow arg="preferred-lifetime" typ="alt { special: enum (infinity) { infinity:0xffffffff }
, value: time
 }"></ArgTableRow>
</ArgTable>
