---
type: Reference
title: "/interface/dot1x/server/active"
description: "RouterOS directory reference for /interface/dot1x/server/active"
timestamp: '2026-10-06'
status: active
tags: [routeros, mikrotik, manual, cli-reference]
resource: https://manual.mikrotik.com/docs/cli-reference/interface/dot1x/server/active.md
sources:
  - resource: https://manual.mikrotik.com/docs/cli-reference/interface/dot1x/server/active.md
---

-----------

## interface/dot1x/server/active 
**Conditions:** !smips
**Type:** Directory

<ArgTable c1="Read-only Argument" c2="Type" c3="Description">
<ArgTableRow arg="interface" typ="iface_enum"></ArgTableRow>
<ArgTableRow arg="username" typ="string"></ArgTableRow>
<ArgTableRow arg="client-mac" typ="macAddr"></ArgTableRow>
<ArgTableRow arg="session-id" typ="string"></ArgTableRow>
<ArgTableRow arg="vlan-id" typ="num"></ArgTableRow>
<ArgTableRow arg="auth-info" typ="string"></ArgTableRow>
</ArgTable>
