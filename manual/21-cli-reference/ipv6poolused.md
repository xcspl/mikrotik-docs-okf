---
type: Reference
title: "/ipv6/pool/used"
description: "RouterOS directory reference for /ipv6/pool/used"
timestamp: '2026-10-06'
status: active
tags: [routeros, mikrotik, manual, cli-reference]
resource: https://manual.mikrotik.com/docs/cli-reference/ipv6/pool/used.md
sources:
  - resource: https://manual.mikrotik.com/docs/cli-reference/ipv6/pool/used.md
---

-----------

## ipv6/pool/used 
**Type:** Directory

<ArgTable c1="Read-only Argument" c2="Type" c3="Description">
<ArgTableRow arg="pool" typ="enum">Name of the pool the prefix is reserved from.</ArgTableRow>
<ArgTableRow arg="prefix" typ="ip6Prefix">IPv6 prefix that is assigned to the client from the pool.</ArgTableRow>
<ArgTableRow arg="owner" typ="string">What reserved the prefix ("DHCP", etc.)</ArgTableRow>
<ArgTableRow arg="info" typ="string">Shows DUID related information received from the client (value in hex). Can contain also a raw timestamp in hex.</ArgTableRow>
</ArgTable>
