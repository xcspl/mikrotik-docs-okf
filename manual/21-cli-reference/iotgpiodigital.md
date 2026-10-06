---
type: Reference
title: "/iot/gpio/digital"
description: "RouterOS directory reference for /iot/gpio/digital"
timestamp: '2026-10-06'
status: active
tags: [routeros, mikrotik, manual, cli-reference]
resource: https://manual.mikrotik.com/docs/cli-reference/iot/gpio/digital.md
sources:
  - resource: https://manual.mikrotik.com/docs/cli-reference/iot/gpio/digital.md
---

-----------

## iot/gpio/digital 
**Syscap:** gpio
**Package:** iot
**Type:** Directory

<ArgTable c1="Flag" c2="Name" c3="Description">
<ArgTableRow arg="X" typ="disabled"></ArgTableRow>
</ArgTable>

<ArgTable c1="Argument" c2="Type" c3="Description">
<ArgTableRow arg="direction" typ="enum (input | output)"></ArgTableRow>
<ArgTableRow arg="output" typ="enum (0 | 1) { 0:0, 1:1 }"></ArgTableRow>
<ArgTableRow arg="script" typ="alt { script: string
 }"></ArgTableRow>
</ArgTable>

<ArgTable c1="Read-only Argument" c2="Type" c3="Description">
<ArgTableRow arg="name" typ="string"></ArgTableRow>
<ArgTableRow arg="input" typ="enum (0 | 1) { 0:0, 1:1 }"></ArgTableRow>
</ArgTable>
