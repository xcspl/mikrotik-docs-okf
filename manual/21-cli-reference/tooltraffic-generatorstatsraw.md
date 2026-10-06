---
type: Reference
title: "/tool/traffic-generator/stats/raw"
description: "RouterOS directory reference for /tool/traffic-generator/stats/raw"
timestamp: '2026-10-06'
status: active
tags: [routeros, mikrotik, manual, cli-reference]
resource: https://manual.mikrotik.com/docs/cli-reference/tool/traffic-generator/stats/raw.md
sources:
  - resource: https://manual.mikrotik.com/docs/cli-reference/tool/traffic-generator/stats/raw.md
---

-----------

## tool/traffic-generator/stats/raw 
**Type:** Directory

<ArgTable c1="Read-only Argument" c2="Type" c3="Description">
<ArgTableRow arg="seq" typ="enum (TOT) { TOT:0xffffffff }"></ArgTableRow>
<ArgTableRow arg="port" typ="composite { p: enum (TOT) { TOT:0xffffffff }
, interface: iface_enum
 }"></ArgTableRow>
<ArgTableRow arg="id" typ="enum (TOT) { TOT:0xffffffff }"></ArgTableRow>
<ArgTableRow arg="tx-packet" typ="num"></ArgTableRow>
<ArgTableRow arg="tx-byte" typ="num"></ArgTableRow>
<ArgTableRow arg="tx-rate" typ="num"></ArgTableRow>
<ArgTableRow arg="rx-packet" typ="num"></ArgTableRow>
<ArgTableRow arg="rx-byte" typ="num"></ArgTableRow>
<ArgTableRow arg="rx-rate" typ="num"></ArgTableRow>
<ArgTableRow arg="rx-ooo" typ="num"></ArgTableRow>
<ArgTableRow arg="rx-bad-csum" typ="num"></ArgTableRow>
<ArgTableRow arg="lost-packet" typ="num"></ArgTableRow>
<ArgTableRow arg="lost-byte" typ="num"></ArgTableRow>
<ArgTableRow arg="lost-rate" typ="num"></ArgTableRow>
<ArgTableRow arg="lost-ratio" typ="string"></ArgTableRow>
<ArgTableRow arg="lat-min" typ="string"></ArgTableRow>
<ArgTableRow arg="lat-avg" typ="string"></ArgTableRow>
<ArgTableRow arg="lat-max" typ="string"></ArgTableRow>
<ArgTableRow arg="jitter" typ="string"></ArgTableRow>
</ArgTable>
