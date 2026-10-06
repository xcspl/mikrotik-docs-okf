---
type: Reference
title: "/iot/lora/joineui"
description: "RouterOS directory reference for /iot/lora/joineui"
timestamp: '2026-10-06'
status: active
tags: [routeros, mikrotik, manual, cli-reference]
resource: https://manual.mikrotik.com/docs/cli-reference/iot/lora/joineui.md
sources:
  - resource: https://manual.mikrotik.com/docs/cli-reference/iot/lora/joineui.md
---

-----------

## iot/lora/joineui 
**Package:** iot
**Type:** Directory

<ArgTable c1="Argument" c2="Type" c3="Description">
<ArgTableRow arg="name" typ="string" mandatory="1"></ArgTableRow>
<ArgTableRow arg="logging" typ="bool"></ArgTableRow>
<ArgTableRow arg="type" typ="enum (whitelist | blacklist) { whitelist:1, blacklist:2 }"></ArgTableRow>
<ArgTableRow arg="joineuis" typ="object { range: composite { min: string
, max: string
 }
 }"></ArgTableRow>
</ArgTable>
