---
type: Reference
title: "/cmr/device/apptraffic"
description: "Application traffic monitor for the selected devices"
timestamp: '2026-10-06'
status: active
tags: [routeros, mikrotik, manual, cli-reference]
resource: https://manual.mikrotik.com/docs/cli-reference/cmr/device/apptraffic.md
sources:
  - resource: https://manual.mikrotik.com/docs/cli-reference/cmr/device/apptraffic.md
---

-----------

## cmr/device/apptraffic 
**Package:** cmr
**Type:** Command

Application traffic monitor for the selected devices.

<ArgTable c1="Argument" c2="Type" c3="Description">
<ArgTableRow arg="labels" typ="object" unset="1">Select the devices to monitor using labels. Supports + and - signs as AND and AND NOT operators, respectively; if no sign is provided, the OR operator is used.</ArgTableRow>
</ArgTable>
