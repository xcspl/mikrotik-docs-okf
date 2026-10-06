---
type: Reference
title: "/user-manager/router"
description: "RouterOS directory reference for /user-manager/router"
timestamp: '2026-10-06'
status: active
tags: [routeros, mikrotik, manual, cli-reference]
resource: https://manual.mikrotik.com/docs/cli-reference/user-manager/router.md
sources:
  - resource: https://manual.mikrotik.com/docs/cli-reference/user-manager/router.md
---

-----------

## user-manager/router 
**Package:** userman-5
**Type:** Directory

<ArgTable c1="Flag" c2="Name" c3="Description">
<ArgTableRow arg="X" typ="disabled"></ArgTableRow>
</ArgTable>

<ArgTable c1="Argument" c2="Type" c3="Description">
<ArgTableRow arg="name" typ="string" mandatory="1"></ArgTableRow>
<ArgTableRow arg="address" typ="address (flags=46/)" mandatory="1"></ArgTableRow>
<ArgTableRow arg="protocol" typ="enum (udp | radsec)"></ArgTableRow>
<ArgTableRow arg="shared-secret" typ="string"></ArgTableRow>
<ArgTableRow arg="coa-port" typ="num"></ArgTableRow>
</ArgTable>
