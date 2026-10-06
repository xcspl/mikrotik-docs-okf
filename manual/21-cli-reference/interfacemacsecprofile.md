---
type: Reference
title: "/interface/macsec/profile"
description: "RouterOS directory reference for /interface/macsec/profile"
timestamp: '2026-10-06'
status: active
tags: [routeros, mikrotik, manual, cli-reference]
resource: https://manual.mikrotik.com/docs/cli-reference/interface/macsec/profile.md
sources:
  - resource: https://manual.mikrotik.com/docs/cli-reference/interface/macsec/profile.md
---

-----------

## interface/macsec/profile 
**Conditions:** !smips
**Type:** Directory

<ArgTable c1="Flag" c2="Name" c3="Description">
<ArgTableRow arg="*" typ="default">default</ArgTableRow>
</ArgTable>

<ArgTable c1="Argument" c2="Type" c3="Description">
<ArgTableRow arg="name" typ="string" mandatory="1"></ArgTableRow>
<ArgTableRow arg="ciphers" typ="multi { cipher: enum (aes-gcm-128 | aes-gcm-xpn-128)
 }" mandatory="1"></ArgTableRow>
<ArgTableRow arg="server-priority" typ="num"></ArgTableRow>
</ArgTable>

<ArgTable c1="Read-only Argument" c2="Type" c3="Description">
<ArgTableRow arg="default-name" typ="string"></ArgTableRow>
</ArgTable>
