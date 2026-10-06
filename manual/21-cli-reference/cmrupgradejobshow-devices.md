---
type: Reference
title: "/cmr/upgrade/job/show-devices"
description: "Shows the devices the selected job covers. A scheduled job resolves its device list only when the job starts, so the output for a job that has not started yet can be empty"
timestamp: '2026-10-06'
status: active
tags: [routeros, mikrotik, manual, cli-reference]
resource: https://manual.mikrotik.com/docs/cli-reference/cmr/upgrade/job/show-devices.md
sources:
  - resource: https://manual.mikrotik.com/docs/cli-reference/cmr/upgrade/job/show-devices.md
---

-----------

## cmr/upgrade/job/show-devices 
**Package:** cmr
**Type:** Command

Shows the devices the selected job covers. A scheduled job resolves its device list only when the job starts, so the output for a job that has not started yet can be empty.

<ArgTable c1="Flag" c2="Name" c3="Description">
<ArgTableRow arg="L" typ="controller">Include the CMR server itself (self-client).</ArgTableRow>
</ArgTable>
