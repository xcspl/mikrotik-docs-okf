---
type: Reference
title: "/ip/dhcp-relay/monitor"
description: "Shows the counters of a DHCP relay"
timestamp: '2026-10-06'
status: active
tags: [routeros, mikrotik, manual, cli-reference]
resource: https://manual.mikrotik.com/docs/cli-reference/ip/dhcp-relay/monitor.md
sources:
  - resource: https://manual.mikrotik.com/docs/cli-reference/ip/dhcp-relay/monitor.md
---

-----------

## ip/dhcp-relay/monitor 
**Type:** Command

Shows the counters of a DHCP relay.

<ArgTable c1="Read-only Argument" c2="Type" c3="Description">
<ArgTableRow arg="requests" typ="num">Number of client requests the relay forwarded to the servers.</ArgTableRow>
<ArgTableRow arg="responses" typ="num">Number of server replies the relay delivered to clients.</ArgTableRow>
</ArgTable>
