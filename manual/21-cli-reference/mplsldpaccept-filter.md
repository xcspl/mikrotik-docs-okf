---
type: Reference
title: "/mpls/ldp/accept-filter"
description: "List of label bindings that should be accepted from LDP neighbors"
timestamp: '2026-10-06'
status: active
tags: [routeros, mikrotik, manual, cli-reference]
resource: https://manual.mikrotik.com/docs/cli-reference/mpls/ldp/accept-filter.md
sources:
  - resource: https://manual.mikrotik.com/docs/cli-reference/mpls/ldp/accept-filter.md
---

-----------

## mpls/ldp/accept-filter 
**Conditions:** !smips
**Type:** Directory

List of label bindings that should be accepted from LDP neighbors.

<ArgTable c1="Flag" c2="Name" c3="Description">
<ArgTableRow arg="X" typ="disabled">disabled</ArgTableRow>
</ArgTable>

<ArgTable c1="Argument" c2="Type" c3="Description">
<ArgTableRow arg="vrf" typ="enum (any) { any:0xffffffff }" unset="1"></ArgTableRow>
<ArgTableRow arg="prefix" typ="address (flags=46/)" unset="1">Prefix to match.</ArgTableRow>
<ArgTableRow arg="neighbor" typ="address (flags=46/)" unset="1">Neighbor to which this filter applies.</ArgTableRow>
<ArgTableRow arg="accept" typ="bool" unset="1">Whether to accept label bindings from the neighbors for the specified prefix. If parameter is unset then matching prefix is not accepted.</ArgTableRow>
</ArgTable>
