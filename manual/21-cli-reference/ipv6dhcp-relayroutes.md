---
type: Reference
title: "/ipv6/dhcp-relay/routes"
description: "Bindings found in the servers' replies by DHCPv6 relays with store-relayed-bindings=yes. The relay adds a route to each delegated prefix through the client. For details, see DHCP Relay"
timestamp: '2026-10-06'
status: active
tags: [routeros, mikrotik, manual, cli-reference]
resource: https://manual.mikrotik.com/docs/cli-reference/ipv6/dhcp-relay/routes.md
sources:
  - resource: https://manual.mikrotik.com/docs/cli-reference/ipv6/dhcp-relay/routes.md
---

-----------

## ipv6/dhcp-relay/routes 
**Type:** Directory

Bindings found in the servers' replies by DHCPv6 relays with `store-relayed-bindings=yes`. The relay adds a route to each delegated prefix through the client. For details, see [DHCP Relay](https://manual.mikrotik.com/docs/network-management/dhcp/relay).

<ArgTable c1="Read-only Argument" c2="Type" c3="Description">
<ArgTableRow arg="relay" typ="enum">DHCPv6 relay that saw the binding.</ArgTableRow>
<ArgTableRow arg="prefix" typ="ip6Prefix">Delegated prefix or assigned address.</ArgTableRow>
<ArgTableRow arg="peer-address" typ="ip6Addr">Address of the client, usually its link-local address, used as the gateway of the route.</ArgTableRow>
<ArgTableRow arg="life-time" typ="time">Lifetime of the binding.</ArgTableRow>
<ArgTableRow arg="last-seen" typ="time">Time since the relay last saw the binding in a reply.</ArgTableRow>
</ArgTable>
