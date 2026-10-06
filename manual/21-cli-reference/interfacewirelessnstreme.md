---
type: Reference
title: "/interface/wireless/nstreme"
description: "RouterOS directory reference for /interface/wireless/nstreme"
timestamp: '2026-10-06'
status: active
tags: [routeros, mikrotik, manual, cli-reference]
resource: https://manual.mikrotik.com/docs/cli-reference/interface/wireless/nstreme.md
sources:
  - resource: https://manual.mikrotik.com/docs/cli-reference/interface/wireless/nstreme.md
---

-----------

## interface/wireless/nstreme 
**Package:** wireless-rep
**Type:** Directory

<ArgTable c1="Argument" c2="Type" c3="Description">
<ArgTableRow arg="enable-nstreme" typ="bool"></ArgTableRow>
<ArgTableRow arg="enable-polling" typ="bool"></ArgTableRow>
<ArgTableRow arg="disable-csma" typ="bool"></ArgTableRow>
<ArgTableRow arg="framer-policy" typ="enum (none | best-fit | exact-size | dynamic-size) { none:0, best-fit:2, exact-size:3, dynamic-size:4 }"></ArgTableRow>
<ArgTableRow arg="framer-limit" typ="num"></ArgTableRow>
</ArgTable>

<ArgTable c1="Read-only Argument" c2="Type" c3="Description">
<ArgTableRow arg="name" typ="string"></ArgTableRow>
</ArgTable>
