---
type: Reference
title: "/ip/cloud/advanced"
description: "Advanced DDNS settings. For an overview, see DDNS"
timestamp: '2026-10-06'
status: active
tags: [routeros, mikrotik, manual, cli-reference]
resource: https://manual.mikrotik.com/docs/cli-reference/ip/cloud/advanced.md
sources:
  - resource: https://manual.mikrotik.com/docs/cli-reference/ip/cloud/advanced.md
---

-----------

## ip/cloud/advanced 
**Type:** Settings Directory

Advanced DDNS settings. For an overview, see [DDNS](https://manual.mikrotik.com/docs/network-management/cloud/#ddns).

<ArgTable c1="Argument" c2="Type" c3="Description">
<ArgTableRow arg="use-local-address" typ="bool">Whether the DNS name points to the router's local address instead of its public address. With `yes`, `dns-name` resolves to the address the router sends its requests from, for example a private address behind NAT, and `public-address` still shows the public address. Default: no.</ArgTableRow>
</ArgTable>
