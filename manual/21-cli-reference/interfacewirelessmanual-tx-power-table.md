---
type: Reference
title: "/interface/wireless/manual-tx-power-table"
description: "RouterOS directory reference for /interface/wireless/manual-tx-power-table"
timestamp: '2026-10-06'
status: active
tags: [routeros, mikrotik, manual, cli-reference]
resource: https://manual.mikrotik.com/docs/cli-reference/interface/wireless/manual-tx-power-table.md
sources:
  - resource: https://manual.mikrotik.com/docs/cli-reference/interface/wireless/manual-tx-power-table.md
---

-----------

## interface/wireless/manual-tx-power-table 
**Package:** wireless-rep
**Type:** Directory

<ArgTable c1="Argument" c2="Type" c3="Description">
<ArgTableRow arg="manual-tx-powers" typ="multi { array-id, array-id, manual-tx-power: composite { rate: enum ()
, tx-power: num [-30 .. 40]
 }
 }"></ArgTableRow>
</ArgTable>

<ArgTable c1="Read-only Argument" c2="Type" c3="Description">
<ArgTableRow arg="name" typ="string"></ArgTableRow>
</ArgTable>
