---
type: Reference
title: "/interface/monitor-traffic"
description: "RouterOS command reference for /interface/monitor-traffic"
timestamp: '2026-10-06'
status: active
tags: [routeros, mikrotik, manual, cli-reference]
resource: https://manual.mikrotik.com/docs/cli-reference/interface/monitor-traffic.md
sources:
  - resource: https://manual.mikrotik.com/docs/cli-reference/interface/monitor-traffic.md
---

-----------

## interface/monitor-traffic 
**Type:** Command

<ArgTable c1="Argument" c2="Type" c3="Description">
<ArgTableRow arg="interface" typ="multi { array-id, interface: iface_enum { aggregate:0 }
 }"></ArgTableRow>
</ArgTable>

<ArgTable c1="Read-only Argument" c2="Type" c3="Description">
<ArgTableRow arg="name" typ="string"></ArgTableRow>
<ArgTableRow arg="rx-packets-per-second" typ="num"></ArgTableRow>
<ArgTableRow arg="rx-bits-per-second" typ="num"></ArgTableRow>
<ArgTableRow arg="fp-rx-packets-per-second" typ="num"></ArgTableRow>
<ArgTableRow arg="fp-rx-bits-per-second" typ="num"></ArgTableRow>
<ArgTableRow arg="rx-drops-per-second" typ="num"></ArgTableRow>
<ArgTableRow arg="rx-errors-per-second" typ="num"></ArgTableRow>
<ArgTableRow arg="tx-packets-per-second" typ="num"></ArgTableRow>
<ArgTableRow arg="tx-bits-per-second" typ="num"></ArgTableRow>
<ArgTableRow arg="fp-tx-packets-per-second" typ="num"></ArgTableRow>
<ArgTableRow arg="fp-tx-bits-per-second" typ="num"></ArgTableRow>
<ArgTableRow arg="tx-drops-per-second" typ="num"></ArgTableRow>
<ArgTableRow arg="tx-queue-drops-per-second" typ="num"></ArgTableRow>
<ArgTableRow arg="tx-errors-per-second" typ="num"></ArgTableRow>
</ArgTable>
