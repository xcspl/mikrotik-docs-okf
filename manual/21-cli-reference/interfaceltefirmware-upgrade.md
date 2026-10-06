---
type: Reference
title: "/interface/lte/firmware-upgrade"
description: "RouterOS command reference for /interface/lte/firmware-upgrade"
timestamp: '2026-10-06'
status: active
tags: [routeros, mikrotik, manual, cli-reference]
resource: https://manual.mikrotik.com/docs/cli-reference/interface/lte/firmware-upgrade.md
sources:
  - resource: https://manual.mikrotik.com/docs/cli-reference/interface/lte/firmware-upgrade.md
---

-----------

## interface/lte/firmware-upgrade 
**Conditions:** !smips
**Type:** Command

<ArgTable c1="Argument" c2="Type" c3="Description">
<ArgTableRow arg="upgrade" typ="bool">perform the upgrade or just check</ArgTableRow>
<ArgTableRow arg="firmware-file" typ="file">path or url for the upgrade image</ArgTableRow>
<ArgTableRow arg="update-channel" typ="enum (stable | testing)">firmware update channel</ArgTableRow>
</ArgTable>

<ArgTable c1="Read-only Argument" c2="Type" c3="Description">
<ArgTableRow arg="installed" typ="string"></ArgTableRow>
<ArgTableRow arg="latest" typ="string"></ArgTableRow>
<ArgTableRow arg="note" typ="string"></ArgTableRow>
<ArgTableRow arg="status" typ="string"></ArgTableRow>
</ArgTable>
