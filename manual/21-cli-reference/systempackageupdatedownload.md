---
type: Reference
title: "/system/package/update/download"
description: "Download the latest available RouterOS packages without installing. A manual reboot is required to apply the update"
timestamp: '2026-10-06'
status: active
tags: [routeros, mikrotik, manual, cli-reference]
resource: https://manual.mikrotik.com/docs/cli-reference/system/package/update/download.md
sources:
  - resource: https://manual.mikrotik.com/docs/cli-reference/system/package/update/download.md
---

-----------

## system/package/update/download 
**Type:** Command

Download the latest available RouterOS packages without installing. A manual reboot is required to apply the update.

<ArgTable c1="Argument" c2="Type" c3="Description">
<ArgTableRow arg="ignore-missing" typ="bool" unset="1">Download only the RouterOS main package, omitting packages that are missing or not uploaded.</ArgTableRow>
</ArgTable>
