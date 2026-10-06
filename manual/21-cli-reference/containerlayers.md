---
type: Reference
title: "/container/layers"
description: "RouterOS directory reference for /container/layers"
timestamp: '2026-10-06'
status: active
tags: [routeros, mikrotik, manual, cli-reference]
resource: https://manual.mikrotik.com/docs/cli-reference/container/layers.md
sources:
  - resource: https://manual.mikrotik.com/docs/cli-reference/container/layers.md
---

-----------

## container/layers 
**Package:** container
**Type:** Directory

<ArgTable c1="Read-only Argument" c2="Type" c3="Description">
<ArgTableRow arg="name" typ="string"></ArgTableRow>
<ArgTableRow arg="layer-dir" typ="string"></ArgTableRow>
<ArgTableRow arg="size" typ="alt { size: num
, size-state: enum (unavailable | pending | done)
 }"></ArgTableRow>
<ArgTableRow arg="type" typ="enum (layer | root-dir)"></ArgTableRow>
<ArgTableRow arg="containers" typ="multi { container: enum
 }"></ArgTableRow>
</ArgTable>
