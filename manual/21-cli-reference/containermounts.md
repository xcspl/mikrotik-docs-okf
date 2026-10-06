---
type: Reference
title: "/container/mounts"
description: "RouterOS directory reference for /container/mounts"
timestamp: '2026-10-06'
status: active
tags: [routeros, mikrotik, manual, cli-reference]
resource: https://manual.mikrotik.com/docs/cli-reference/container/mounts.md
sources:
  - resource: https://manual.mikrotik.com/docs/cli-reference/container/mounts.md
---

-----------

## container/mounts 
**Package:** container
**Type:** Directory

<ArgTable c1="Flag" c2="Name" c3="Description">
<ArgTableRow arg="X" typ="disabled"></ArgTableRow>
</ArgTable>

<ArgTable c1="Argument" c2="Type" c3="Description">
<ArgTableRow arg="list" typ="enum" mandatory="1"></ArgTableRow>
<ArgTableRow arg="src" typ="file"></ArgTableRow>
<ArgTableRow arg="dst" typ="string" mandatory="1"></ArgTableRow>
<ArgTableRow arg="mode" typ="enum (rw | ro | rw,noexec | ro,noexec)"></ArgTableRow>
</ArgTable>
