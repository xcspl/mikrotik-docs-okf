---
type: Reference
title: "/system/keymat-provider/qkd-get-key-with-ids"
description: "RouterOS command reference for /system/keymat-provider/qkd-get-key-with-ids"
timestamp: '2026-10-06'
status: active
tags: [routeros, mikrotik, manual, cli-reference]
resource: https://manual.mikrotik.com/docs/cli-reference/system/keymat-provider/qkd-get-key-with-ids.md
sources:
  - resource: https://manual.mikrotik.com/docs/cli-reference/system/keymat-provider/qkd-get-key-with-ids.md
---

-----------

## system/keymat-provider/qkd-get-key-with-ids 
**Type:** Command

<ArgTable c1="Argument" c2="Type" c3="Description">
<ArgTableRow arg="key-ids" typ="multi { array-id, key-id: string
 }"></ArgTableRow>
</ArgTable>

<ArgTable c1="Read-only Argument" c2="Type" c3="Description">
<ArgTableRow arg="keys" typ="object { qkd-key: super { key-id: string
, [key] : string
 }
 }"></ArgTableRow>
</ArgTable>
