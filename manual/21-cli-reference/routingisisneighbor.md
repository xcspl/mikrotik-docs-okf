---
type: Reference
title: "/routing/isis/neighbor"
description: "RouterOS directory reference for /routing/isis/neighbor"
timestamp: '2026-10-06'
status: active
tags: [routeros, mikrotik, manual, cli-reference]
resource: https://manual.mikrotik.com/docs/cli-reference/routing/isis/neighbor.md
sources:
  - resource: https://manual.mikrotik.com/docs/cli-reference/routing/isis/neighbor.md
---

-----------

## routing/isis/neighbor 
**Type:** Directory

<ArgTable c1="Flag" c2="Name" c3="Description">
<ArgTableRow arg="D" typ="dynamic">dynamic</ArgTableRow>
</ArgTable>

<ArgTable c1="Argument" c2="Type" c3="Description">
<ArgTableRow arg="instance" typ="enum"></ArgTableRow>
<ArgTableRow arg="interface" typ="iface_enum"></ArgTableRow>
<ArgTableRow arg="level-type" typ="enum (l1 | l2)"></ArgTableRow>
<ArgTableRow arg="snpa" typ="macAddr"></ArgTableRow>
<ArgTableRow arg="srcid" typ="string"></ArgTableRow>
<ArgTableRow arg="state" typ="enum (init | up)" unset="1"></ArgTableRow>
</ArgTable>
