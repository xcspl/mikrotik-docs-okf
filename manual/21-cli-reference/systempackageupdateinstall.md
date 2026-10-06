---
type: Reference
title: "/system/package/update/install"
description: "Download and install the latest available RouterOS packages, followed by an automatic reboot"
timestamp: '2026-10-06'
status: active
tags: [routeros, mikrotik, manual, cli-reference]
resource: https://manual.mikrotik.com/docs/cli-reference/system/package/update/install.md
sources:
  - resource: https://manual.mikrotik.com/docs/cli-reference/system/package/update/install.md
---

-----------

## system/package/update/install 
**Type:** Command

Download and install the latest available RouterOS packages, followed by an automatic reboot.

<ArgTable c1="Argument" c2="Type" c3="Description">
<ArgTableRow arg="ignore-missing" typ="bool" unset="1">Install only the RouterOS main package, omitting packages that are missing or not uploaded.</ArgTableRow>
</ArgTable>
