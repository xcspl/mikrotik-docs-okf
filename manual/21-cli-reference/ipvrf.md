---
type: Reference
title: "/ip/vrf"
description: "RouterOS directory reference for /ip/vrf"
timestamp: '2026-10-06'
status: active
tags: [routeros, mikrotik, manual, cli-reference]
resource: https://manual.mikrotik.com/docs/cli-reference/ip/vrf.md
sources:
  - resource: https://manual.mikrotik.com/docs/cli-reference/ip/vrf.md
---

-----------

## ip/vrf 
**Type:** Directory

<ArgTable c1="Flag" c2="Name" c3="Description">
<ArgTableRow arg="X" typ="disabled">disabled</ArgTableRow>
<ArgTableRow arg="*" typ="builtin">builtin</ArgTableRow>
</ArgTable>

<ArgTable c1="Argument" c2="Type" c3="Description">
<ArgTableRow arg="name" typ="string" mandatory="1"></ArgTableRow>
<ArgTableRow arg="interfaces" typ="object { interface: iface_enum
 }" mandatory="1"></ArgTableRow>
</ArgTable>
