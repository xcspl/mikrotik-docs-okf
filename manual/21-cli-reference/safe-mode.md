---
type: Reference
title: "/safe-mode"
description: "RouterOS settings reference for /safe-mode"
timestamp: '2026-10-06'
status: active
tags: [routeros, mikrotik, manual, cli-reference]
resource: https://manual.mikrotik.com/docs/cli-reference/safe-mode.md
sources:
  - resource: https://manual.mikrotik.com/docs/cli-reference/safe-mode.md
---

-----------

## safe-mode 
**Type:** Settings Directory

<ArgTable c1="Read-only Argument" c2="Type" c3="Description">
<ArgTableRow arg="enabled" typ="bool">indicates if safe mode is enabled</ArgTableRow>
<ArgTableRow arg="user" typ="string">user name of the current safe mode session</ArgTableRow>
<ArgTableRow arg="current" typ="bool">indicates if safe mode is enabled for the current session</ArgTableRow>
<ArgTableRow arg="owner" typ="string">safe mode session owner</ArgTableRow>
</ArgTable>
