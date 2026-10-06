---
type: Reference
title: "/ip/ipsec/key/rsa"
description: "RouterOS directory reference for /ip/ipsec/key/rsa"
timestamp: '2026-10-06'
status: active
tags: [routeros, mikrotik, manual, cli-reference]
resource: https://manual.mikrotik.com/docs/cli-reference/ip/ipsec/key/rsa.md
sources:
  - resource: https://manual.mikrotik.com/docs/cli-reference/ip/ipsec/key/rsa.md
---

-----------

## ip/ipsec/key/rsa 
**Type:** Directory

<ArgTable c1="Flag" c2="Name" c3="Description">
<ArgTableRow arg="P" typ="private-key">Whether the item contains a private key.</ArgTableRow>
<ArgTableRow arg="R" typ="rsa">Whether the item uses an RSA key.</ArgTableRow>
</ArgTable>

<ArgTable c1="Argument" c2="Type" c3="Description">
<ArgTableRow arg="name" typ="string">Key name.</ArgTableRow>
</ArgTable>

<ArgTable c1="Read-only Argument" c2="Type" c3="Description">
<ArgTableRow arg="key-size" typ="num">RSA key size in bits.</ArgTableRow>
</ArgTable>
