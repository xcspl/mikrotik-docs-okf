---
type: Reference
title: "/interface/wifi/sniffer"
description: "RouterOS command reference for /interface/wifi/sniffer"
timestamp: '2026-10-06'
status: active
tags: [routeros, mikrotik, manual, cli-reference]
resource: https://manual.mikrotik.com/docs/cli-reference/interface/wifi/sniffer.md
sources:
  - resource: https://manual.mikrotik.com/docs/cli-reference/interface/wifi/sniffer.md
---

-----------

## interface/wifi/sniffer 
**Type:** Command

<ArgTable c1="Argument" c2="Type" c3="Description">
<ArgTableRow arg="stream-address" typ="address (flags=46v)"></ArgTableRow>
<ArgTableRow arg="stream-rate" typ="num"></ArgTableRow>
<ArgTableRow arg="stream-port" typ="num" unset="1"></ArgTableRow>
<ArgTableRow arg="pcap-file" typ="string" unset="1"></ArgTableRow>
<ArgTableRow arg="pcap-size-limit" typ="num" unset="1"></ArgTableRow>
<ArgTableRow arg="filter" typ="string" unset="1"></ArgTableRow>
<ArgTableRow arg="show-frame" typ="enum (no | yes | radiotap)" unset="1"></ArgTableRow>
</ArgTable>

<ArgTable c1="Read-only Argument" c2="Type" c3="Description">
<ArgTableRow arg="num" typ="num"></ArgTableRow>
<ArgTableRow arg="wlan.addr1" typ="macAddr"></ArgTableRow>
<ArgTableRow arg="wlan.addr2" typ="macAddr"></ArgTableRow>
<ArgTableRow arg="wlan.addr3" typ="macAddr"></ArgTableRow>
<ArgTableRow arg="size" typ="num"></ArgTableRow>
<ArgTableRow arg="type" typ="string"></ArgTableRow>
<ArgTableRow arg="ssid" typ="string"></ArgTableRow>
<ArgTableRow arg="raw" typ="string"></ArgTableRow>
</ArgTable>
