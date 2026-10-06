---
type: Reference
title: "/tool/traffic-generator/inject-pcap"
description: "RouterOS command reference for /tool/traffic-generator/inject-pcap"
timestamp: '2026-10-06'
status: active
tags: [routeros, mikrotik, manual, cli-reference]
resource: https://manual.mikrotik.com/docs/cli-reference/tool/traffic-generator/inject-pcap.md
sources:
  - resource: https://manual.mikrotik.com/docs/cli-reference/tool/traffic-generator/inject-pcap.md
---

-----------

## tool/traffic-generator/inject-pcap 
**Type:** Command

<ArgTable c1="Argument" c2="Type" c3="Description">
<ArgTableRow arg="interface" typ="iface_enum"></ArgTableRow>
<ArgTableRow arg="pcap-file" typ="file"></ArgTableRow>
<ArgTableRow arg="speed-multiplier" typ="num"></ArgTableRow>
<ArgTableRow arg="loop" typ="bool"></ArgTableRow>
</ArgTable>

<ArgTable c1="Read-only Argument" c2="Type" c3="Description">
<ArgTableRow arg="iteration" typ="num"></ArgTableRow>
<ArgTableRow arg="tx-packets" typ="num"></ArgTableRow>
<ArgTableRow arg="tx-bytes" typ="num"></ArgTableRow>
</ArgTable>
