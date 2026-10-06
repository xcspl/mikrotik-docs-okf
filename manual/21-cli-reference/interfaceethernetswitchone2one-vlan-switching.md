---
type: Reference
title: "/interface/ethernet/switch/one2one-vlan-switching"
description: "1:1 VLAN switching can be used to replace the regular L2 bridging for matched packets. When a packet hits a 1:1 VLAN switching table entry, the destination port information in the entry is assigned to the packet. The"
timestamp: '2026-10-06'
status: active
tags: [routeros, mikrotik, manual, cli-reference]
resource: https://manual.mikrotik.com/docs/cli-reference/interface/ethernet/switch/one2one-vlan-switching.md
sources:
  - resource: https://manual.mikrotik.com/docs/cli-reference/interface/ethernet/switch/one2one-vlan-switching.md
---

-----------

## interface/ethernet/switch/one2one-vlan-switching 
**Syscap:** musicswitch
**Type:** Directory

1:1 VLAN switching can be used to replace the regular L2 bridging for matched packets. When a packet hits a 1:1 VLAN switching table entry, the destination port information in the entry is assigned to the packet. The matched destination information in the UFDB and MFDB entries no longer applies to the packet.

<ArgTable c1="Flag" c2="Name" c3="Description">
<ArgTableRow arg="X" typ="disabled"></ArgTableRow>
<ArgTableRow arg="I" typ="invalid"></ArgTableRow>
</ArgTable>

<ArgTable c1="Argument" c2="Type" c3="Description">
<ArgTableRow arg="dst-port" typ="alt { port: enum
, trunk: enum
 }" mandatory="1">Destination port for matched 1:1 VLAN switching packets.</ArgTableRow>
<ArgTableRow arg="service-vid" typ="num">Matching service VLAN id for 1:1 VLAN switching.</ArgTableRow>
<ArgTableRow arg="customer-vid" typ="num">Matching customer VLAN id for 1:1 VLAN switching.</ArgTableRow>
</ArgTable>
