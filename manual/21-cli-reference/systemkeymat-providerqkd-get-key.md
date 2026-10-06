---
type: Reference
title: "/system/keymat-provider/qkd-get-key"
description: "RouterOS command reference for /system/keymat-provider/qkd-get-key"
timestamp: '2026-10-06'
status: active
tags: [routeros, mikrotik, manual, cli-reference]
resource: https://manual.mikrotik.com/docs/cli-reference/system/keymat-provider/qkd-get-key.md
sources:
  - resource: https://manual.mikrotik.com/docs/cli-reference/system/keymat-provider/qkd-get-key.md
---

-----------

## system/keymat-provider/qkd-get-key 
**Type:** Command

<ArgTable c1="Argument" c2="Type" c3="Description">
<ArgTableRow arg="additional-sae-ids" typ="multi { array-id, sae-id: string
 }">additional SAEs which will also get the generated key</ArgTableRow>
<ArgTableRow arg="number" typ="num">number of keys to generate</ArgTableRow>
</ArgTable>

<ArgTable c1="Read-only Argument" c2="Type" c3="Description">
<ArgTableRow arg="keys" typ="object { qkd-key: super { key-id: string
, [key] : string
 }
 }"></ArgTableRow>
</ArgTable>
