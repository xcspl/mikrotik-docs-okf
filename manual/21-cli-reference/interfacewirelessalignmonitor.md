---
type: Reference
title: "/interface/wireless/align/monitor"
description: "RouterOS command reference for /interface/wireless/align/monitor"
timestamp: '2026-10-06'
status: active
tags: [routeros, mikrotik, manual, cli-reference]
resource: https://manual.mikrotik.com/docs/cli-reference/interface/wireless/align/monitor.md
sources:
  - resource: https://manual.mikrotik.com/docs/cli-reference/interface/wireless/align/monitor.md
---

-----------

## interface/wireless/align/monitor 
**Package:** wireless-rep
**Type:** Command

<ArgTable c1="Flag" c2="Name" c3="Description">
<ArgTableRow arg="A" typ="access-point"></ArgTableRow>
</ArgTable>

<ArgTable c1="Argument" c2="Type" c3="Description">
<ArgTableRow arg="interface" typ="iface_enum"></ArgTableRow>
</ArgTable>

<ArgTable c1="Read-only Argument" c2="Type" c3="Description">
<ArgTableRow arg="address" typ="macAddr"></ArgTableRow>
<ArgTableRow arg="ssid" typ="string"></ArgTableRow>
<ArgTableRow arg="rxq" typ="num"></ArgTableRow>
<ArgTableRow arg="avg-rxq" typ="num"></ArgTableRow>
<ArgTableRow arg="last-rx" typ="num"></ArgTableRow>
<ArgTableRow arg="txq" typ="num"></ArgTableRow>
<ArgTableRow arg="last-tx" typ="num"></ArgTableRow>
<ArgTableRow arg="correct" typ="num"></ArgTableRow>
</ArgTable>
