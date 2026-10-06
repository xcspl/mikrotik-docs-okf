---
type: Reference
title: "/system/package/local-update/update-package-source"
description: "The server from which to get the package is defined in this list"
timestamp: '2026-10-06'
status: active
tags: [routeros, mikrotik, manual, cli-reference]
resource: https://manual.mikrotik.com/docs/cli-reference/system/package/local-update/update-package-source.md
sources:
  - resource: https://manual.mikrotik.com/docs/cli-reference/system/package/local-update/update-package-source.md
---

-----------

## system/package/local-update/update-package-source 
**Type:** Directory

The server from which to get the package is defined in this list.

<ArgTable c1="Argument" c2="Type" c3="Description">
<ArgTableRow arg="address" typ="alt { ipv6: ip6Addr
, ip: ipAddr
 }" mandatory="1">IP address of the local package server.</ArgTableRow>
<ArgTableRow arg="user" typ="string" mandatory="1">Username for accessing the local package server.</ArgTableRow>
<ArgTableRow arg="password" typ="string" mandatory="1">Password for accessing the local package server.</ArgTableRow>
</ArgTable>
