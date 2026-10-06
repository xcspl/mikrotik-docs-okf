---
type: Reference
title: "/routing/isis/lsp"
description: "RouterOS directory reference for /routing/isis/lsp"
timestamp: '2026-10-06'
status: active
tags: [routeros, mikrotik, manual, cli-reference]
resource: https://manual.mikrotik.com/docs/cli-reference/routing/isis/lsp.md
sources:
  - resource: https://manual.mikrotik.com/docs/cli-reference/routing/isis/lsp.md
---

-----------

## routing/isis/lsp 
**Type:** Directory

<ArgTable c1="Flag" c2="Name" c3="Description">
<ArgTableRow arg="I" typ="inactive">inactive</ArgTableRow>
<ArgTableRow arg="D" typ="dynamic">dynamic</ArgTableRow>
</ArgTable>

<ArgTable c1="Argument" c2="Type" c3="Description">
<ArgTableRow arg="instance" typ="enum"></ArgTableRow>
<ArgTableRow arg="level" typ="enum (l1 | l2)"></ArgTableRow>
<ArgTableRow arg="lsp-id" typ="string"></ArgTableRow>
<ArgTableRow arg="age" typ="num"></ArgTableRow>
<ArgTableRow arg="checksum" typ="num"></ArgTableRow>
<ArgTableRow arg="sequence" typ="num"></ArgTableRow>
<ArgTableRow arg="body" typ="string" unset="1"></ArgTableRow>
</ArgTable>
