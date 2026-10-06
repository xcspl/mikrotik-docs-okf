---
type: Reference
title: "/system/package/update/check-for-updates"
description: "Check the MikroTik download server for a newer RouterOS version in the selected release channel"
timestamp: '2026-10-06'
status: active
tags: [routeros, mikrotik, manual, cli-reference]
resource: https://manual.mikrotik.com/docs/cli-reference/system/package/update/check-for-updates.md
sources:
  - resource: https://manual.mikrotik.com/docs/cli-reference/system/package/update/check-for-updates.md
---

-----------

## system/package/update/check-for-updates 
**Type:** Command

Check the MikroTik download server for a newer RouterOS version in the selected release channel.

<ArgTable c1="Argument" c2="Type" c3="Description">
<ArgTableRow arg="fetch-changelog" typ="switch">Whether to fetch the changelog along with the update check.</ArgTableRow>
</ArgTable>

<ArgTable c1="Read-only Argument" c2="Type" c3="Description">
<ArgTableRow arg="changelog" typ="string">Changelog text for the latest available version.</ArgTableRow>
</ArgTable>
