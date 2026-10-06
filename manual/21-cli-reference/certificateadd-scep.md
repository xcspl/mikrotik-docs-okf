---
type: Reference
title: "/certificate/add-scep"
description: "RouterOS command reference for /certificate/add-scep"
timestamp: '2026-10-06'
status: active
tags: [routeros, mikrotik, manual, cli-reference]
resource: https://manual.mikrotik.com/docs/cli-reference/certificate/add-scep.md
sources:
  - resource: https://manual.mikrotik.com/docs/cli-reference/certificate/add-scep.md
---

-----------

## certificate/add-scep 
**Type:** Command

<ArgTable c1="Argument" c2="Type" c3="Description">
<ArgTableRow arg="name" typ="string"></ArgTableRow>
<ArgTableRow arg="ca-identity" typ="string"></ArgTableRow>
<ArgTableRow arg="template" typ="enum"></ArgTableRow>
<ArgTableRow arg="scep-url" typ="string"></ArgTableRow>
<ArgTableRow arg="challenge-password" typ="string"></ArgTableRow>
<ArgTableRow arg="on-smart-card" typ="bool">stores private key on smart card if hardware supports it</ArgTableRow>
<ArgTableRow arg="refresh" typ="bool">check certificate expiry and refresh it if expired</ArgTableRow>
</ArgTable>
