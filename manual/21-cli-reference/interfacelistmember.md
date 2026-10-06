---
type: Reference
title: "/interface/list/member"
description: "List of static interface members. Dynamically added interfaces from include and exclude statements do not appear in this sub-menu"
timestamp: '2026-10-06'
status: active
tags: [routeros, mikrotik, manual, cli-reference]
resource: https://manual.mikrotik.com/docs/cli-reference/interface/list/member.md
sources:
  - resource: https://manual.mikrotik.com/docs/cli-reference/interface/list/member.md
---

-----------

## interface/list/member 
**Type:** Directory

List of static interface members. Dynamically added interfaces from `include` and `exclude` statements do not appear in this sub-menu.

:::info
Care must be taken when working with bridges and lists. Adding a bridge as a member is not the same as adding all its ports. Adding all slave ports as members is not the same as adding the bridge itself. This can impact the functionality of Neighbour Discovery.
:::

<ArgTable c1="Flag" c2="Name" c3="Description">
<ArgTableRow arg="X" typ="disabled">Member entry is disabled.</ArgTableRow>
<ArgTableRow arg="D" typ="dynamic">Dynamically added member.</ArgTableRow>
</ArgTable>

<ArgTable c1="Argument" c2="Type" c3="Description">
<ArgTableRow arg="list" typ="enum" mandatory="1">Name of the interface list to which the member belongs.</ArgTableRow>
<ArgTableRow arg="interface" typ="iface_enum" mandatory="1">Name of the interface that is a member of the list.</ArgTableRow>
</ArgTable>

<ArgTable c1="Read-only Argument" c2="Type" c3="Description">
<ArgTableRow arg="dynamic" typ="bool">Whether the member was added dynamically.</ArgTableRow>
</ArgTable>
