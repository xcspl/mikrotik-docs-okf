---
type: Reference
title: "/iot/modbus/security-rules"
description: "RouterOS directory reference for /iot/modbus/security-rules"
timestamp: '2026-10-06'
status: active
tags: [routeros, mikrotik, manual, cli-reference]
resource: https://manual.mikrotik.com/docs/cli-reference/iot/modbus/security-rules.md
sources:
  - resource: https://manual.mikrotik.com/docs/cli-reference/iot/modbus/security-rules.md
---

-----------

## iot/modbus/security-rules 
**Package:** iot
**Type:** Directory

<ArgTable c1="Flag" c2="Name" c3="Description">
<ArgTableRow arg="X" typ="disabled"></ArgTableRow>
</ArgTable>

<ArgTable c1="Argument" c2="Type" c3="Description">
<ArgTableRow arg="ip-range" typ="ipRange" mandatory="1"></ArgTableRow>
<ArgTableRow arg="allowed-function-codes" typ="multi { array-id, value: num
 }" mandatory="1"></ArgTableRow>
</ArgTable>
