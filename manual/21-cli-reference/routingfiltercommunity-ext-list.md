---
type: Reference
title: "/routing/filter/community-ext-list"
description: "RouterOS directory reference for /routing/filter/community-ext-list"
timestamp: '2026-10-06'
status: active
tags: [routeros, mikrotik, manual, cli-reference]
resource: https://manual.mikrotik.com/docs/cli-reference/routing/filter/community-ext-list.md
sources:
  - resource: https://manual.mikrotik.com/docs/cli-reference/routing/filter/community-ext-list.md
---

-----------

## routing/filter/community-ext-list 
**Type:** Directory

<ArgTable c1="Flag" c2="Name" c3="Description">
<ArgTableRow arg="X" typ="disabled">disabled</ArgTableRow>
</ArgTable>

<ArgTable c1="Argument" c2="Type" c3="Description">
<ArgTableRow arg="list" typ="enum" mandatory="1">Reference name.</ArgTableRow>
<ArgTableRow arg="communities" typ="object">
List of extended communities expressed as a **raw** integer value or in the typed format: `type:value`, where type can be:
- `rt` - route-target
- `soo` -  site of origin.

The value depends on the type.
</ArgTableRow>
<ArgTableRow arg="regexp" typ="string">Regexp matcher to match communities. The community set with only the regexp parameter cannot be used to append/delete communities.</ArgTableRow>
</ArgTable>
