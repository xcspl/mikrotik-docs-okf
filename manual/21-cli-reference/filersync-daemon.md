---
type: Reference
title: "/file/rsync-daemon"
description: "RouterOS settings reference for /file/rsync-daemon"
timestamp: '2026-10-06'
status: active
tags: [routeros, mikrotik, manual, cli-reference]
resource: https://manual.mikrotik.com/docs/cli-reference/file/rsync-daemon.md
sources:
  - resource: https://manual.mikrotik.com/docs/cli-reference/file/rsync-daemon.md
---

-----------

## file/rsync-daemon 
**Package:** rose-storage
**Type:** Settings Directory

<ArgTable c1="Argument" c2="Type" c3="Description">
<ArgTableRow arg="enabled" typ="bool">Whether the router runs the rsync daemon that accepts [`sync`](https://manual.mikrotik.com/docs/cli-reference/file/sync/) transfers from other routers; required on the receiving device. Default: no.</ArgTableRow>
</ArgTable>
