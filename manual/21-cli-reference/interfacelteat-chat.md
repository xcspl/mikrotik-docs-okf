---
type: Reference
title: "/interface/lte/at-chat"
description: "RouterOS command reference for /interface/lte/at-chat"
timestamp: '2026-10-06'
status: active
tags: [routeros, mikrotik, manual, cli-reference]
resource: https://manual.mikrotik.com/docs/cli-reference/interface/lte/at-chat.md
sources:
  - resource: https://manual.mikrotik.com/docs/cli-reference/interface/lte/at-chat.md
---

-----------

## interface/lte/at-chat 
**Conditions:** !smips
**Type:** Command

<ArgTable c1="Argument" c2="Type" c3="Description">
<ArgTableRow arg="input" typ="string">sends command to modem and waits for any output before returning</ArgTableRow>
<ArgTableRow arg="wait" typ="alt { wait: enum (no | yes) { no:0, yes:3 }
 }">always wait 3s</ArgTableRow>
</ArgTable>

<ArgTable c1="Read-only Argument" c2="Type" c3="Description">
<ArgTableRow arg="output" typ="string"></ArgTableRow>
</ArgTable>
