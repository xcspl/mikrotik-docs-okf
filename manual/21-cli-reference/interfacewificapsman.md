---
type: Reference
title: "/interface/wifi/capsman"
description: "RouterOS settings reference for /interface/wifi/capsman"
timestamp: '2026-10-06'
status: active
tags: [routeros, mikrotik, manual, cli-reference]
resource: https://manual.mikrotik.com/docs/cli-reference/interface/wifi/capsman.md
sources:
  - resource: https://manual.mikrotik.com/docs/cli-reference/interface/wifi/capsman.md
---

-----------

## interface/wifi/capsman 
**Type:** Settings Directory

<ArgTable c1="Argument" c2="Type" c3="Description">
<ArgTableRow arg="enabled" typ="enum (yes | no)"></ArgTableRow>
<ArgTableRow arg="interfaces" typ="multi { array-id, interface: iface_enum
 }" unset="1"></ArgTableRow>
<ArgTableRow arg="ca-certificate" typ="enum (auto | none) { auto:0 }" unset="1"></ArgTableRow>
<ArgTableRow arg="certificate" typ="enum (auto) { auto:0 }" unset="1"></ArgTableRow>
<ArgTableRow arg="require-peer-certificate" typ="bool" unset="1"></ArgTableRow>
<ArgTableRow arg="package-path" typ="string" unset="1"></ArgTableRow>
<ArgTableRow arg="upgrade-policy" typ="enum (none | suggest-same-version | require-same-version)" unset="1"></ArgTableRow>
</ArgTable>

<ArgTable c1="Read-only Argument" c2="Type" c3="Description">
<ArgTableRow arg="generated-ca-certificate" typ="enum (none)"></ArgTableRow>
<ArgTableRow arg="generated-certificate" typ="enum (none)"></ArgTableRow>
</ArgTable>
