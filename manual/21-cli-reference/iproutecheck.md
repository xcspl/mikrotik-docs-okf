---
type: Reference
title: "/ip/route/check"
description: "RouterOS command reference for /ip/route/check"
timestamp: '2026-10-06'
status: active
tags: [routeros, mikrotik, manual, cli-reference]
resource: https://manual.mikrotik.com/docs/cli-reference/ip/route/check.md
sources:
  - resource: https://manual.mikrotik.com/docs/cli-reference/ip/route/check.md
---

-----------

## ip/route/check 
**Type:** Command

<ArgTable c1="Argument" c2="Type" c3="Description">
<ArgTableRow arg="src-ip" typ="ipAddr"></ArgTableRow>
<ArgTableRow arg="dst-ip" typ="ipAddr"></ArgTableRow>
</ArgTable>

<ArgTable c1="Read-only Argument" c2="Type" c3="Description">
<ArgTableRow arg="status" typ="string"></ArgTableRow>
<ArgTableRow arg="interface" typ="iface_enum"></ArgTableRow>
<ArgTableRow arg="nexthop" typ="ipAddr"></ArgTableRow>
</ArgTable>
