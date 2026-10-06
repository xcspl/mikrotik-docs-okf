---
type: Reference
title: "/ip/dns/adlist/pause"
description: "Stops blocking by all adlists for the given time, for example /ip/dns/adlist/pause duration=10m. Blocking resumes by itself when the time runs out"
timestamp: '2026-10-06'
status: active
tags: [routeros, mikrotik, manual, cli-reference]
resource: https://manual.mikrotik.com/docs/cli-reference/ip/dns/adlist/pause.md
sources:
  - resource: https://manual.mikrotik.com/docs/cli-reference/ip/dns/adlist/pause.md
---

-----------

## ip/dns/adlist/pause 
**Type:** Command

Stops blocking by all adlists for the given time, for example `/ip/dns/adlist/pause duration=10m`. Blocking resumes by itself when the time runs out.

<ArgTable c1="Argument" c2="Type" c3="Description">
<ArgTableRow arg="duration" typ="time">How long to stop blocking. `duration=0` ends an active pause.</ArgTableRow>
</ArgTable>
