---
type: Reference
title: "/snmp/community"
description: "RouterOS directory reference for /snmp/community"
timestamp: '2026-10-06'
status: active
tags: [routeros, mikrotik, manual, cli-reference]
resource: https://manual.mikrotik.com/docs/cli-reference/snmp/community.md
sources:
  - resource: https://manual.mikrotik.com/docs/cli-reference/snmp/community.md
---

-----------

## snmp/community 
**Type:** Directory

<ArgTable c1="Flag" c2="Name" c3="Description">
<ArgTableRow arg="*" typ="default">default</ArgTableRow>
<ArgTableRow arg="X" typ="disabled">disabled</ArgTableRow>
</ArgTable>

<ArgTable c1="Argument" c2="Type" c3="Description">
<ArgTableRow arg="name" typ="string"></ArgTableRow>
<ArgTableRow arg="addresses" typ="object { address: alt { ipv6: ip6Prefix
, ip: ipPrefix
 }
 }"></ArgTableRow>
<ArgTableRow arg="security" typ="enum (none | authorized | private) { none:0, authorized:1, private:2 }"></ArgTableRow>
<ArgTableRow arg="read-access" typ="bool"></ArgTableRow>
<ArgTableRow arg="write-access" typ="bool"></ArgTableRow>
<ArgTableRow arg="denied-oids" typ="multi { array-id, oid: string
 }"></ArgTableRow>
<ArgTableRow arg="authentication-protocol" typ="enum (MD5 | SHA1 | SHA256 | SHA384 | SHA512) { MD5:0, SHA1:1, SHA256:2, SHA384:3, SHA512:4 }"></ArgTableRow>
<ArgTableRow arg="encryption-protocol" typ="enum (DES | AES)"></ArgTableRow>
<ArgTableRow arg="authentication-password" typ="string"></ArgTableRow>
<ArgTableRow arg="encryption-password" typ="string"></ArgTableRow>
</ArgTable>
