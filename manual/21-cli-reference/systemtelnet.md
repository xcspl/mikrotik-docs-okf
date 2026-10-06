---
type: Reference
title: "/system/telnet"
description: "RouterOS command reference for /system/telnet"
timestamp: '2026-10-06'
status: active
tags: [routeros, mikrotik, manual, cli-reference]
resource: https://manual.mikrotik.com/docs/cli-reference/system/telnet.md
sources:
  - resource: https://manual.mikrotik.com/docs/cli-reference/system/telnet.md
---

-----------

## system/telnet 
**Type:** Command

<ArgTable c1="Argument" c2="Type" c3="Description">
<ArgTableRow arg="address" typ="alt { ip-address: ipAddr
, ipv6-address: composite { addr: ip6Addr
, interface: [ iface_enum]
 }
 }"></ArgTableRow>
<ArgTableRow arg="port" typ="num"></ArgTableRow>
<ArgTableRow arg="vrf" typ="enum"></ArgTableRow>
</ArgTable>
