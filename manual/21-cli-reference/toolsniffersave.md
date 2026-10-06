---
type: Reference
title: "/tool/sniffer/save"
description: "Writes the packets in memory to a file. Since RouterOS 7.20 the file is always in pcapng format, also with a .pcap extension; it carries the interface name, the direction and nanosecond timestamps of each packet. See"
timestamp: '2026-10-06'
status: active
tags: [routeros, mikrotik, manual, cli-reference]
resource: https://manual.mikrotik.com/docs/cli-reference/tool/sniffer/save.md
sources:
  - resource: https://manual.mikrotik.com/docs/cli-reference/tool/sniffer/save.md
---

-----------

## tool/sniffer/save 
**Type:** Command

Writes the packets in memory to a file. Since RouterOS 7.20 the file is always in pcapng format, also with a `.pcap` extension; it carries the interface name, the direction and nanosecond timestamps of each packet. See [Packet sniffer](https://manual.mikrotik.com/docs/diagnostics-monitoring-and-troubleshooting/packet-sniffer).

<ArgTable c1="Argument" c2="Type" c3="Description">
<ArgTableRow arg="file-name" typ="file">Name of the file to write, for example `capture.pcap`.</ArgTableRow>
</ArgTable>
