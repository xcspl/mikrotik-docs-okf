---
type: Reference
title: "/cmr/upgrade/trigger"
description: "Starts the job of a chosen rule right away, without waiting for the schedule-time. Only one upgrade job runs at a time; triggering another rule while a job is in progress places the new job in a queued state until"
timestamp: '2026-10-06'
status: active
tags: [routeros, mikrotik, manual, cli-reference]
resource: https://manual.mikrotik.com/docs/cli-reference/cmr/upgrade/trigger.md
sources:
  - resource: https://manual.mikrotik.com/docs/cli-reference/cmr/upgrade/trigger.md
---

-----------

## cmr/upgrade/trigger 
**Package:** cmr
**Type:** Command

Starts the job of a chosen rule right away, without waiting for the schedule-time. Only one upgrade job runs at a time; triggering another rule while a job is in progress places the new job in a [queued state](https://manual.mikrotik.com/docs/cli-reference/cmr/upgrade/job#cmr-upgrade-job) until the current job finishes.

Triggering forces an early upgrade of the rule's covered devices: the job runs immediately and upgrades each covered device that has a newer version available, without waiting for the schedule-time. Covered devices that are already up to date are skipped, so the run's counter counts only the upgraded ones. To upgrade a single device regardless of its rule, see [`/cmr/device/upgrade`](https://manual.mikrotik.com/docs/cli-reference/cmr/device/upgrade).
