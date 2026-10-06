---
type: Reference
title: "/ipv6/nd/proxy"
description: "An IPv6 Neighbor Discovery Proxy allows a router or host to respond to Neighbor Discovery (RFC 4861) messages on behalf of another node. This enables communication across different network segments as if they were on"
timestamp: '2026-10-06'
status: active
tags: [routeros, mikrotik, manual, cli-reference]
resource: https://manual.mikrotik.com/docs/cli-reference/ipv6/nd/proxy.md
sources:
  - resource: https://manual.mikrotik.com/docs/cli-reference/ipv6/nd/proxy.md
---

-----------

## ipv6/nd/proxy 
**Type:** Directory

An IPv6 Neighbor Discovery Proxy allows a router or host to respond to Neighbor Discovery ([RFC 4861](https://tools.ietf.org/html/rfc4861)) messages on behalf of another node. This enables communication across different network segments as if they were on the same link. In RouterOS, the proxy can be enabled for a single IPv6 address and works per interface.

<ArgTable c1="Flag" c2="Name" c3="Description">
<ArgTableRow arg="X" typ="disabled">disabled</ArgTableRow>
</ArgTable>

<ArgTable c1="Argument" c2="Type" c3="Description">
<ArgTableRow arg="address" typ="ip6Addr">IPv6 address the proxy takes ownership of.</ArgTableRow>
<ArgTableRow arg="interface" typ="iface_enum">Interface on which the proxy operates for this IPv6 address.</ArgTableRow>
</ArgTable>
