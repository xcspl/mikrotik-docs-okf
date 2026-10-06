---
type: Reference
title: "/routing/pimsm/bsr/rp-set"
description: "RouterOS directory reference for /routing/pimsm/bsr/rp-set"
timestamp: '2026-10-06'
status: active
tags: [routeros, mikrotik, manual, cli-reference]
resource: https://manual.mikrotik.com/docs/cli-reference/routing/pimsm/bsr/rp-set.md
sources:
  - resource: https://manual.mikrotik.com/docs/cli-reference/routing/pimsm/bsr/rp-set.md
---

-----------

## routing/pimsm/bsr/rp-set 
**Conditions:** !smips
**Type:** Directory

<ArgTable c1="Read-only Argument" c2="Type" c3="Description">
<ArgTableRow arg="instance" typ="enum"></ArgTableRow>
<ArgTableRow arg="group" typ="address (flags=46/v)"></ArgTableRow>
<ArgTableRow arg="rp.address" typ="object { address: address (flags=46)
 }"></ArgTableRow>
<ArgTableRow arg="rp.priority" typ="object { priority: num
 }"></ArgTableRow>
<ArgTableRow arg="rp.timeout" typ="object { timeout: time
 }"></ArgTableRow>
</ArgTable>
