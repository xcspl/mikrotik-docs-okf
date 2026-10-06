---
type: Reference
title: "/iot/bluetooth"
description: "RouterOS directory reference for /iot/bluetooth"
timestamp: '2026-10-06'
status: active
tags: [routeros, mikrotik, manual, cli-reference]
resource: https://manual.mikrotik.com/docs/cli-reference/iot/bluetooth.md
sources:
  - resource: https://manual.mikrotik.com/docs/cli-reference/iot/bluetooth.md
---

-----------

## iot/bluetooth 
**Package:** iot
**Type:** Directory

<ArgTable c1="Flag" c2="Name" c3="Description">
<ArgTableRow arg="X" typ="offline"></ArgTableRow>
</ArgTable>

<ArgTable c1="Argument" c2="Type" c3="Description">
<ArgTableRow arg="name" typ="string"></ArgTableRow>
<ArgTableRow arg="random-static-address" typ="macAddr"></ArgTableRow>
<ArgTableRow arg="antenna" typ="enum (internal | external) { internal:0, external:1 }"></ArgTableRow>
</ArgTable>

<ArgTable c1="Read-only Argument" c2="Type" c3="Description">
<ArgTableRow arg="public-address" typ="macAddr"></ArgTableRow>
<ArgTableRow arg="rx-bytes" typ="num"></ArgTableRow>
<ArgTableRow arg="tx-bytes" typ="num"></ArgTableRow>
<ArgTableRow arg="rx-errors" typ="num"></ArgTableRow>
<ArgTableRow arg="tx-errors" typ="num"></ArgTableRow>
<ArgTableRow arg="rx-evt" typ="num"></ArgTableRow>
<ArgTableRow arg="tx-cmd" typ="num"></ArgTableRow>
<ArgTableRow arg="rx-acl" typ="num"></ArgTableRow>
<ArgTableRow arg="tx-acl" typ="num"></ArgTableRow>
</ArgTable>
