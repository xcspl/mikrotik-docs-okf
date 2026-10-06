---
type: Reference
title: "/caps-man/registration-table"
description: "RouterOS directory reference for /caps-man/registration-table"
timestamp: '2026-10-06'
status: active
tags: [routeros, mikrotik, manual, cli-reference]
resource: https://manual.mikrotik.com/docs/cli-reference/caps-man/registration-table.md
sources:
  - resource: https://manual.mikrotik.com/docs/cli-reference/caps-man/registration-table.md
---

-----------

## caps-man/registration-table 
**Package:** wireless-rep
**Type:** Directory

<ArgTable c1="Read-only Argument" c2="Type" c3="Description">
<ArgTableRow arg="interface" typ="iface_enum"></ArgTableRow>
<ArgTableRow arg="ssid" typ="string"></ArgTableRow>
<ArgTableRow arg="mac-address" typ="macAddr"></ArgTableRow>
<ArgTableRow arg="radio-name" typ="string"></ArgTableRow>
<ArgTableRow arg="tx-rate" typ="string"></ArgTableRow>
<ArgTableRow arg="rx-rate" typ="string"></ArgTableRow>
<ArgTableRow arg="tx-signal" typ="num"></ArgTableRow>
<ArgTableRow arg="rx-signal" typ="num"></ArgTableRow>
<ArgTableRow arg="uptime" typ="time"></ArgTableRow>
<ArgTableRow arg="packets" typ="composite { tx: num
, rx: num
 }"></ArgTableRow>
<ArgTableRow arg="bytes" typ="composite { tx: num
, rx: num
 }"></ArgTableRow>
<ArgTableRow arg="tx-rate-set" typ="string"></ArgTableRow>
<ArgTableRow arg="eap-identity" typ="string"></ArgTableRow>
<ArgTableRow arg="vlan-id" typ="num"></ArgTableRow>
<ArgTableRow arg="last-ip" typ="ipAddr"></ArgTableRow>
</ArgTable>
