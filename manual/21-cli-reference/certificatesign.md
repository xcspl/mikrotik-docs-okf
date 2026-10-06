---
type: Reference
title: "/certificate/sign"
description: "RouterOS command reference for /certificate/sign"
timestamp: '2026-10-06'
status: active
tags: [routeros, mikrotik, manual, cli-reference]
resource: https://manual.mikrotik.com/docs/cli-reference/certificate/sign.md
sources:
  - resource: https://manual.mikrotik.com/docs/cli-reference/certificate/sign.md
---

-----------

## certificate/sign 
**Type:** Command

<ArgTable c1="Argument" c2="Type" c3="Description">
<ArgTableRow arg="name" typ="string"></ArgTableRow>
<ArgTableRow arg="ca-crl-host" typ="multi { array-id, host: string
 }">adds CRL URL to created certificate</ArgTableRow>
<ArgTableRow arg="ca-on-smart-card" typ="bool">stores CA's private key on smart card</ArgTableRow>
<ArgTableRow arg="ca" typ="enum">issuer CA</ArgTableRow>
</ArgTable>

<ArgTable c1="Read-only Argument" c2="Type" c3="Description">
<ArgTableRow arg="progress" typ="string"></ArgTableRow>
</ArgTable>
