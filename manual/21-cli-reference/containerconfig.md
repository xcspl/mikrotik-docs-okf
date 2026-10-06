---
type: Reference
title: "/container/config"
description: "RouterOS settings reference for /container/config"
timestamp: '2026-10-06'
status: active
tags: [routeros, mikrotik, manual, cli-reference]
resource: https://manual.mikrotik.com/docs/cli-reference/container/config.md
sources:
  - resource: https://manual.mikrotik.com/docs/cli-reference/container/config.md
---

-----------

## container/config 
**Package:** container
**Type:** Settings Directory

<ArgTable c1="Argument" c2="Type" c3="Description">
<ArgTableRow arg="registry-url" typ="string"></ArgTableRow>
<ArgTableRow arg="username" typ="string"></ArgTableRow>
<ArgTableRow arg="password" typ="string"></ArgTableRow>
<ArgTableRow arg="layer-dir" typ="file"></ArgTableRow>
<ArgTableRow arg="tmpdir" typ="file"></ArgTableRow>
<ArgTableRow arg="memory-high" typ="num"></ArgTableRow>
<ArgTableRow arg="memory-max" typ="num"></ArgTableRow>
<ArgTableRow arg="swap-max" typ="num"></ArgTableRow>
</ArgTable>

<ArgTable c1="Read-only Argument" c2="Type" c3="Description">
<ArgTableRow arg="assumed-registry-url" typ="string"></ArgTableRow>
<ArgTableRow arg="memory-current" typ="num"></ArgTableRow>
<ArgTableRow arg="swap-current" typ="num"></ArgTableRow>
</ArgTable>
