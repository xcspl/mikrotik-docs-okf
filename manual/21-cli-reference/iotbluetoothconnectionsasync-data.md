---
type: Reference
title: "/iot/bluetooth/connections/async-data"
description: "RouterOS directory reference for /iot/bluetooth/connections/async-data"
timestamp: '2026-10-06'
status: active
tags: [routeros, mikrotik, manual, cli-reference]
resource: https://manual.mikrotik.com/docs/cli-reference/iot/bluetooth/connections/async-data.md
sources:
  - resource: https://manual.mikrotik.com/docs/cli-reference/iot/bluetooth/connections/async-data.md
---

-----------

## iot/bluetooth/connections/async-data 
**Package:** iot
**Type:** Directory

<ArgTable c1="Read-only Argument" c2="Type" c3="Description">
<ArgTableRow arg="pdev" typ="string"></ArgTableRow>
<ArgTableRow arg="uuid" typ="string"></ArgTableRow>
<ArgTableRow arg="data-text" typ="string"></ArgTableRow>
<ArgTableRow arg="data-hex" typ="string"></ArgTableRow>
<ArgTableRow arg="data-bytes" typ="multi { array-id, value: num
 }"></ArgTableRow>
<ArgTableRow arg="type" typ="enum (notification | indication) { notification:0x01, indication:0x02 }"></ArgTableRow>
<ArgTableRow arg="time" typ="date"></ArgTableRow>
</ArgTable>
