---
type: Reference
title: "/tool/sniffer/host"
description: "The addresses that took part in the traffic of the last capture, with their rates and byte counts. See Packet sniffer"
timestamp: '2026-10-06'
status: active
tags: [routeros, mikrotik, manual, cli-reference]
resource: https://manual.mikrotik.com/docs/cli-reference/tool/sniffer/host.md
sources:
  - resource: https://manual.mikrotik.com/docs/cli-reference/tool/sniffer/host.md
---

-----------

## tool/sniffer/host 
**Type:** Directory

The addresses that took part in the traffic of the last capture, with their rates and byte counts. See [Packet sniffer](https://manual.mikrotik.com/docs/diagnostics-monitoring-and-troubleshooting/packet-sniffer).

<ArgTable c1="Read-only Argument" c2="Type" c3="Description">
<ArgTableRow arg="address" typ="ipAddr">Address seen in the captured packets.</ArgTableRow>
<ArgTableRow arg="rate" typ="composite { in: num
, out: num
 }">Rate of the address's captured traffic, in bits per second, as two values: in (to the address) and out (from the address). The rates are calculated when the capture stops; while the sniffer runs, they show 0.</ArgTableRow>
<ArgTableRow arg="peak-rate" typ="composite { in: num
, out: num
 }">Highest rate of the address's captured traffic during the capture, in bits per second (in/out), calculated when the capture stops.</ArgTableRow>
<ArgTableRow arg="total" typ="composite { in: num
, out: num
 }">Captured bytes of the address's traffic: in (to the address) and out (from the address).</ArgTableRow>
</ArgTable>
