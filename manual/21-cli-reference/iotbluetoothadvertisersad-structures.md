---
type: Reference
title: "/iot/bluetooth/advertisers/ad-structures"
description: "RouterOS directory reference for /iot/bluetooth/advertisers/ad-structures"
timestamp: '2026-10-06'
status: active
tags: [routeros, mikrotik, manual, cli-reference]
resource: https://manual.mikrotik.com/docs/cli-reference/iot/bluetooth/advertisers/ad-structures.md
sources:
  - resource: https://manual.mikrotik.com/docs/cli-reference/iot/bluetooth/advertisers/ad-structures.md
---

-----------

## iot/bluetooth/advertisers/ad-structures 
**Package:** iot
**Type:** Directory

<ArgTable c1="Argument" c2="Type" c3="Description">
<ArgTableRow arg="name" typ="string" mandatory="1"></ArgTableRow>
<ArgTableRow arg="type" typ="enum (short-local-name | complete-local-name | service-data | manufacturer-data) { short-local-name:8, complete-local-name:9, service-data:22, manufacturer-data:255 }" mandatory="1"></ArgTableRow>
<ArgTableRow arg="data" typ="string" mandatory="1"></ArgTableRow>
</ArgTable>
