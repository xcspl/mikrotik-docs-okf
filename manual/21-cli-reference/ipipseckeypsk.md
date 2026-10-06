---
type: Reference
title: "/ip/ipsec/key/psk"
description: "RouterOS directory reference for /ip/ipsec/key/psk"
timestamp: '2026-10-06'
status: active
tags: [routeros, mikrotik, manual, cli-reference]
resource: https://manual.mikrotik.com/docs/cli-reference/ip/ipsec/key/psk.md
sources:
  - resource: https://manual.mikrotik.com/docs/cli-reference/ip/ipsec/key/psk.md
---

-----------

## ip/ipsec/key/psk 
**Type:** Directory

<ArgTable c1="Argument" c2="Type" c3="Description">
<ArgTableRow arg="peer" typ="enum" mandatory="1">Peer name to associate the PSK with.</ArgTableRow>
<ArgTableRow arg="id" typ="string" mandatory="1">Peer identifier string.</ArgTableRow>
<ArgTableRow arg="key" typ="string" mandatory="1">Pre-shared key value.</ArgTableRow>
</ArgTable>
