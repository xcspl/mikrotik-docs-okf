---
type: Reference
title: "/cmr/upgrade/job/run-next"
description: "Runs the next scheduled upgrade job right away. The job starts as a new run, and the originally scheduled job remains scheduled. Only one upgrade job runs at a time, so a job started while another job is already in"
timestamp: '2026-10-06'
status: active
tags: [routeros, mikrotik, manual, cli-reference]
resource: https://manual.mikrotik.com/docs/cli-reference/cmr/upgrade/job/run-next.md
sources:
  - resource: https://manual.mikrotik.com/docs/cli-reference/cmr/upgrade/job/run-next.md
---

-----------

## cmr/upgrade/job/run-next 
**Package:** cmr
**Type:** Command

Runs the next scheduled upgrade job right away. The job starts as a new run, and the originally scheduled job remains scheduled. Only one upgrade job runs at a time, so a job started while another job is already in progress is queued, not interrupted.
