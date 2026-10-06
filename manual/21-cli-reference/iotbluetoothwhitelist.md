---
type: Reference
title: "/iot/bluetooth/whitelist"
description: "RouterOS directory reference for /iot/bluetooth/whitelist"
timestamp: '2026-10-06'
status: active
tags: [routeros, mikrotik, manual, cli-reference]
resource: https://manual.mikrotik.com/docs/cli-reference/iot/bluetooth/whitelist.md
sources:
  - resource: https://manual.mikrotik.com/docs/cli-reference/iot/bluetooth/whitelist.md
---

-----------

## iot/bluetooth/whitelist 
**Package:** iot
**Type:** Directory

<ArgTable c1="Flag" c2="Name" c3="Description">
<ArgTableRow arg="X" typ="disabled"></ArgTableRow>
</ArgTable>

<ArgTable c1="Argument" c2="Type" c3="Description">
<ArgTableRow arg="device" typ="enum" mandatory="1"></ArgTableRow>
<ArgTableRow arg="address-type" typ="enum (public | random | any) { public:0, random:1, any:2 }" mandatory="1"></ArgTableRow>
<ArgTableRow arg="address" typ="string" mandatory="1"></ArgTableRow>
</ArgTable>
