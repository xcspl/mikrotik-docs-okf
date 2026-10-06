---
type: Reference
title: "/interface/pppoe-client/scan"
description: "PPPoE Scanner allows scanning all active PPPoE servers in the layer2 broadcast domain"
timestamp: '2026-10-06'
status: active
tags: [routeros, mikrotik, manual, cli-reference]
resource: https://manual.mikrotik.com/docs/cli-reference/interface/pppoe-client/scan.md
sources:
  - resource: https://manual.mikrotik.com/docs/cli-reference/interface/pppoe-client/scan.md
---

-----------

## interface/pppoe-client/scan 
**Type:** Command

PPPoE Scanner allows scanning all active PPPoE servers in the layer2 broadcast domain.

<ArgTable c1="Argument" c2="Type" c3="Description">
<ArgTableRow arg="interface" typ="iface_enum">Interface to scan for PPPoE servers on.</ArgTableRow>
</ArgTable>

<ArgTable c1="Read-only Argument" c2="Type" c3="Description">
<ArgTableRow arg="service" typ="string">Service name configured on the server.</ArgTableRow>
<ArgTableRow arg="mac-address" typ="macAddr">MAC address of the detected server.</ArgTableRow>
<ArgTableRow arg="ac-name" typ="string">Name of the Access Concentrator.</ArgTableRow>
</ArgTable>
