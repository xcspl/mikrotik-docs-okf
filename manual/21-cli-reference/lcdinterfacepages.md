---
type: Reference
title: "/lcd/interface/pages"
description: "RouterOS directory reference for /lcd/interface/pages"
timestamp: '2026-10-06'
status: active
tags: [routeros, mikrotik, manual, cli-reference]
resource: https://manual.mikrotik.com/docs/cli-reference/lcd/interface/pages.md
sources:
  - resource: https://manual.mikrotik.com/docs/cli-reference/lcd/interface/pages.md
---

-----------

## lcd/interface/pages 
**Conditions:** !smips
**Syscap:** lcd
**Type:** Directory

<ArgTable c1="Flag" c2="Name" c3="Description">
<ArgTableRow arg="*" typ="default">default</ArgTableRow>
</ArgTable>

<ArgTable c1="Argument" c2="Type" c3="Description">
<ArgTableRow arg="interfaces" typ="multi { array-id, interface: iface_enum
 }" mandatory="1"></ArgTableRow>
</ArgTable>
