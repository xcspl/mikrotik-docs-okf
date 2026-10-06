---
type: Reference
title: "/system/logging/action/clear"
description: "Empties the buffer of a memory action, for example /system/logging/action/clear action=memory for the default buffer. A buffer with memory-stop-on-full=yes accepts new entries again after it is cleared. A disk action"
timestamp: '2026-10-06'
status: active
tags: [routeros, mikrotik, manual, cli-reference]
resource: https://manual.mikrotik.com/docs/cli-reference/system/logging/action/clear.md
sources:
  - resource: https://manual.mikrotik.com/docs/cli-reference/system/logging/action/clear.md
---

-----------

## system/logging/action/clear 
**Type:** Command

Empties the buffer of a memory action, for example `/system/logging/action/clear action=memory` for the default buffer. A buffer with `memory-stop-on-full=yes` accepts new entries again after it is cleared. A disk action refuses with `cleanup not supported on this target`. See [`/system/logging/action`](https://manual.mikrotik.com/docs/cli-reference/system/logging/action/) and [Log](https://manual.mikrotik.com/docs/diagnostics-monitoring-and-troubleshooting/log/).

<ArgTable c1="Argument" c2="Type" c3="Description">
<ArgTableRow arg="action" typ="enum">Name of the memory action whose buffer to empty.</ArgTableRow>
</ArgTable>
