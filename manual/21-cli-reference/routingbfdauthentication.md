---
type: Reference
title: "/routing/bfd/authentication"
description: "RouterOS directory reference for /routing/bfd/authentication"
timestamp: '2026-10-06'
status: active
tags: [routeros, mikrotik, manual, cli-reference]
resource: https://manual.mikrotik.com/docs/cli-reference/routing/bfd/authentication.md
sources:
  - resource: https://manual.mikrotik.com/docs/cli-reference/routing/bfd/authentication.md
---

-----------

## routing/bfd/authentication 
**Conditions:** BFD_AUTHENTICATION
**Type:** Directory

<ArgTable c1="Flag" c2="Name" c3="Description">
<ArgTableRow arg="X" typ="disabled">disabled</ArgTableRow>
<ArgTableRow arg="I" typ="inactive">inactive</ArgTableRow>
<ArgTableRow arg="T" typ="transmit">transmit</ArgTableRow>
</ArgTable>

<ArgTable c1="Argument" c2="Type" c3="Description">
<ArgTableRow arg="keyring" typ="enum" mandatory="1"></ArgTableRow>
<ArgTableRow arg="key-id" typ="num" mandatory="1"></ArgTableRow>
<ArgTableRow arg="type" typ="enum (none | simple-password | keyed-md5 | meticulous-keyed-md5 | keyed-sha1 | meticulous-keyed-sha1)" mandatory="1"></ArgTableRow>
<ArgTableRow arg="key" typ="string"></ArgTableRow>
<ArgTableRow arg="transmit-after" typ="date"></ArgTableRow>
<ArgTableRow arg="accept-before" typ="date"></ArgTableRow>
</ArgTable>
