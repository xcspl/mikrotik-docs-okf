---
type: Reference
title: "/queue/interface"
description: "RouterOS directory reference for /queue/interface"
timestamp: '2026-10-06'
status: active
tags: [routeros, mikrotik, manual, cli-reference]
resource: https://manual.mikrotik.com/docs/cli-reference/queue/interface.md
sources:
  - resource: https://manual.mikrotik.com/docs/cli-reference/queue/interface.md
---

-----------

## queue/interface 
**Type:** Directory

<ArgTable c1="Argument" c2="Type" c3="Description">
<ArgTableRow arg="queue" typ="enum (no-queue) { no-queue:0 }"></ArgTableRow>
</ArgTable>

<ArgTable c1="Read-only Argument" c2="Type" c3="Description">
<ArgTableRow arg="interface" typ="iface_enum"></ArgTableRow>
<ArgTableRow arg="default-queue" typ="enum (no-queue) { no-queue:0 }"></ArgTableRow>
<ArgTableRow arg="active-queue" typ="enum (no-queue | queue-tree) { no-queue:0, queue-tree:0xfffffff9 }"></ArgTableRow>
</ArgTable>
