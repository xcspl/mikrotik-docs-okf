---
type: Reference
title: "/cmr/layout/add-devices"
description: "This command adds multiple devices to the topology in bulk"
timestamp: '2026-10-06'
status: active
tags: [routeros, mikrotik, manual, cli-reference]
resource: https://manual.mikrotik.com/docs/cli-reference/cmr/layout/add-devices.md
sources:
  - resource: https://manual.mikrotik.com/docs/cli-reference/cmr/layout/add-devices.md
---

-----------

## cmr/layout/add-devices 
**Package:** cmr
**Type:** Command

This command adds multiple devices to the topology in bulk.

<ArgTable c1="Argument" c2="Type" c3="Description">
<ArgTableRow arg="labels" typ="object" unset="1">Select devices that should be added to the topology using labels. Supports + and - signs as AND and AND NOT operators, respectively; if no sign is provided, the OR operator is used. (default value: **all**)</ArgTableRow>
<ArgTableRow arg="devices" typ="multi { array-id, device: enum
 }" unset="1">Select specific devices that should be added to the topology.</ArgTableRow>
</ArgTable>
