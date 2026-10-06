---
type: Reference
title: "/interface/wifi/dashboard/show-clients"
description: "RouterOS command reference for /interface/wifi/dashboard/show-clients"
timestamp: '2026-10-06'
status: active
tags: [routeros, mikrotik, manual, cli-reference]
resource: https://manual.mikrotik.com/docs/cli-reference/interface/wifi/dashboard/show-clients.md
sources:
  - resource: https://manual.mikrotik.com/docs/cli-reference/interface/wifi/dashboard/show-clients.md
---

-----------

## interface/wifi/dashboard/show-clients 
**Type:** Command

<ArgTable c1="Flag" c2="Name" c3="Description">
<ArgTableRow arg="A" typ="active"></ArgTableRow>
</ArgTable>

<ArgTable c1="Argument" c2="Type" c3="Description">
<ArgTableRow arg="interface" typ="multi { array-id, interface: iface_enum
 }" unset="1"></ArgTableRow>
<ArgTableRow arg="address" typ="macAddr" unset="1"></ArgTableRow>
<ArgTableRow arg="bssid" typ="macAddr" unset="1"></ArgTableRow>
<ArgTableRow arg="time" typ="time" unset="1"></ArgTableRow>
<ArgTableRow arg="time-start" typ="date" unset="1"></ArgTableRow>
<ArgTableRow arg="time-end" typ="date" unset="1"></ArgTableRow>
<ArgTableRow arg="event" typ="enum (connected | disconnected | failed)" unset="1"></ArgTableRow>
</ArgTable>

<ArgTable c1="Read-only Argument" c2="Type" c3="Description">
<ArgTableRow arg="address" typ="macAddr"></ArgTableRow>
<ArgTableRow arg="dhcp-address" typ="address"></ArgTableRow>
<ArgTableRow arg="dhcp-hostname" typ="string"></ArgTableRow>
<ArgTableRow arg="last-ap" typ="macAddr"></ArgTableRow>
<ArgTableRow arg="conn" typ="num"></ArgTableRow>
<ArgTableRow arg="disconn" typ="num"></ArgTableRow>
<ArgTableRow arg="fail" typ="num"></ArgTableRow>
</ArgTable>
