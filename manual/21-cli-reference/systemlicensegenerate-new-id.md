---
type: Reference
title: "/system/license/generate-new-id"
description: "Generates a new unique system ID for a CHR instance. Use after the first boot and before requesting a trial license when deploying multiple CHR instances from the same disk image to avoid identical system IDs"
timestamp: '2026-10-06'
status: active
tags: [routeros, mikrotik, manual, cli-reference]
resource: https://manual.mikrotik.com/docs/cli-reference/system/license/generate-new-id.md
sources:
  - resource: https://manual.mikrotik.com/docs/cli-reference/system/license/generate-new-id.md
---

-----------

## system/license/generate-new-id 
**Syscap:** chr
**Type:** Command

Generates a new unique system ID for a CHR instance. Use after the first boot and before requesting a trial license when deploying multiple CHR instances from the same disk image to avoid identical system IDs.

:::warning
This command must only be used on a CHR running the Free license level. Do not use it after a trial or paid license has been applied.
:::
