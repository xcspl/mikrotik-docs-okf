---
type: Reference
title: "/interface/wireless/channels"
description: "RouterOS directory reference for /interface/wireless/channels"
timestamp: '2026-10-06'
status: active
tags: [routeros, mikrotik, manual, cli-reference]
resource: https://manual.mikrotik.com/docs/cli-reference/interface/wireless/channels.md
sources:
  - resource: https://manual.mikrotik.com/docs/cli-reference/interface/wireless/channels.md
---

-----------

## interface/wireless/channels 
**Package:** wireless-rep
**Type:** Directory

<ArgTable c1="Flag" c2="Name" c3="Description">
<ArgTableRow arg="X" typ="disabled"></ArgTableRow>
</ArgTable>

<ArgTable c1="Argument" c2="Type" c3="Description">
<ArgTableRow arg="list" typ="enum" mandatory="1"></ArgTableRow>
<ArgTableRow arg="name" typ="string"></ArgTableRow>
<ArgTableRow arg="frequency" typ="num" mandatory="1"></ArgTableRow>
<ArgTableRow arg="width" typ="num" mandatory="1"></ArgTableRow>
<ArgTableRow arg="band" typ="enum (2ghz-b | 2ghz-onlyg | 2ghz-b/g | 5ghz-a | 5ghz-onlyn | 5ghz-a/n | 2ghz-onlyn | 2ghz-b/g/n | 2ghz-g/n | 5ghz-a/n/ac | 5ghz-n/ac | 5ghz-onlyac)" mandatory="1"></ArgTableRow>
<ArgTableRow arg="extension-channel" typ="enum (disabled | Ce | eC | Ceee | eCee | eeCe | eeeC)"></ArgTableRow>
</ArgTable>
