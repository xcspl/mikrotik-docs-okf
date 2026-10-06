---
type: Reference
title: "/interface/ethernet/switch/policer-qos-map"
description: "RouterOS directory reference for /interface/ethernet/switch/policer-qos-map"
timestamp: '2026-10-06'
status: active
tags: [routeros, mikrotik, manual, cli-reference]
resource: https://manual.mikrotik.com/docs/cli-reference/interface/ethernet/switch/policer-qos-map.md
sources:
  - resource: https://manual.mikrotik.com/docs/cli-reference/interface/ethernet/switch/policer-qos-map.md
---

-----------

## interface/ethernet/switch/policer-qos-map 
**Syscap:** musicswitch
**Type:** Directory

<ArgTable c1="Flag" c2="Name" c3="Description">
<ArgTableRow arg="I" typ="invalid"></ArgTableRow>
</ArgTable>

<ArgTable c1="Argument" c2="Type" c3="Description">
<ArgTableRow arg="dscp-for-yellow" typ="num">Policer DSCP remapping value for yellow packets.</ArgTableRow>
<ArgTableRow arg="pcp-for-yellow" typ="num">Policer PCP remapping value for yellow packets.</ArgTableRow>
<ArgTableRow arg="dei-for-yellow" typ="num">Policer DEI remapping value for yellow packets.</ArgTableRow>
<ArgTableRow arg="dscp-for-red" typ="num">Policer DSCP remapping value for red packets.</ArgTableRow>
<ArgTableRow arg="pcp-for-red" typ="num">Policer PCP remapping value for red packets.</ArgTableRow>
<ArgTableRow arg="dei-for-red" typ="num">Policer DEI remapping value for red packets.</ArgTableRow>
</ArgTable>

<ArgTable c1="Read-only Argument" c2="Type" c3="Description">
<ArgTableRow arg="priority" typ="num"></ArgTableRow>
</ArgTable>
