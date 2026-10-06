---
type: Reference
title: "/certificate/scep-server"
description: "RouterOS directory reference for /certificate/scep-server"
timestamp: '2026-10-06'
status: active
tags: [routeros, mikrotik, manual, cli-reference]
resource: https://manual.mikrotik.com/docs/cli-reference/certificate/scep-server.md
sources:
  - resource: https://manual.mikrotik.com/docs/cli-reference/certificate/scep-server.md
---

-----------

## certificate/scep-server 
**Type:** Directory

<ArgTable c1="Flag" c2="Name" c3="Description">
<ArgTableRow arg="X" typ="disabled">disabled</ArgTableRow>
</ArgTable>

<ArgTable c1="Argument" c2="Type" c3="Description">
<ArgTableRow arg="ca-cert" typ="enum" mandatory="1"></ArgTableRow>
<ArgTableRow arg="next-ca-cert" typ="enum (none) { none:0 }"></ArgTableRow>
<ArgTableRow arg="path" typ="string" mandatory="1"></ArgTableRow>
<ArgTableRow arg="days-valid" typ="num"></ArgTableRow>
<ArgTableRow arg="request-lifetime" typ="time"></ArgTableRow>
</ArgTable>
