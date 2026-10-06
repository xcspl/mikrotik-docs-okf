---
type: Reference
title: "/routing/pimsm/bsr/candidate"
description: "RouterOS directory reference for /routing/pimsm/bsr/candidate"
timestamp: '2026-10-06'
status: active
tags: [routeros, mikrotik, manual, cli-reference]
resource: https://manual.mikrotik.com/docs/cli-reference/routing/pimsm/bsr/candidate.md
sources:
  - resource: https://manual.mikrotik.com/docs/cli-reference/routing/pimsm/bsr/candidate.md
---

-----------

## routing/pimsm/bsr/candidate 
**Conditions:** !smips
**Type:** Directory

<ArgTable c1="Flag" c2="Name" c3="Description">
<ArgTableRow arg="X" typ="disabled">disabled</ArgTableRow>
<ArgTableRow arg="I" typ="inactive">inactive</ArgTableRow>
</ArgTable>

<ArgTable c1="Argument" c2="Type" c3="Description">
<ArgTableRow arg="instance" typ="enum"></ArgTableRow>
<ArgTableRow arg="address" typ="address (flags=46i)"></ArgTableRow>
<ArgTableRow arg="scope4" typ="address (flags=4/)" unset="1"></ArgTableRow>
<ArgTableRow arg="scope6" typ="num" unset="1"></ArgTableRow>
<ArgTableRow arg="priority" typ="num"></ArgTableRow>
<ArgTableRow arg="hash-mask-length" typ="num"></ArgTableRow>
</ArgTable>

<ArgTable c1="Read-only Argument" c2="Type" c3="Description">
<ArgTableRow arg="state" typ="enum (candidate | pending | elected)"></ArgTableRow>
</ArgTable>
