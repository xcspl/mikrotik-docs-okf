---
type: Reference
title: "/ip/ssh/known-hosts"
description: "RouterOS directory reference for /ip/ssh/known-hosts"
timestamp: '2026-10-06'
status: active
tags: [routeros, mikrotik, manual, cli-reference]
resource: https://manual.mikrotik.com/docs/cli-reference/ip/ssh/known-hosts.md
sources:
  - resource: https://manual.mikrotik.com/docs/cli-reference/ip/ssh/known-hosts.md
---

-----------

## ip/ssh/known-hosts 
**Type:** Directory

<ArgTable c1="Argument" c2="Type" c3="Description">
<ArgTableRow arg="host" typ="ip6Addr"></ArgTableRow>
<ArgTableRow arg="key" typ="string"></ArgTableRow>
</ArgTable>

<ArgTable c1="Read-only Argument" c2="Type" c3="Description">
<ArgTableRow arg="key-type" typ="enum (rsa | ed25519)"></ArgTableRow>
<ArgTableRow arg="fingerprint" typ="string"></ArgTableRow>
</ArgTable>
