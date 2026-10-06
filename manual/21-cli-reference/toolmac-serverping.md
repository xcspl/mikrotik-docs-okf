---
type: Reference
title: "/tool/mac-server/ping"
description: "MAC ping server settings. With the server enabled, the router answers pings sent to its MAC address (/ping ). For examples, see MAC server"
timestamp: '2026-10-06'
status: active
tags: [routeros, mikrotik, manual, cli-reference]
resource: https://manual.mikrotik.com/docs/cli-reference/tool/mac-server/ping.md
sources:
  - resource: https://manual.mikrotik.com/docs/cli-reference/tool/mac-server/ping.md
---

-----------

## tool/mac-server/ping 
**Type:** Settings Directory

MAC ping server settings. With the server enabled, the router answers pings sent to its MAC address (`/ping <MAC address>`). For examples, see [MAC server](https://manual.mikrotik.com/docs/management-tools/mac-server).

<ArgTable c1="Argument" c2="Type" c3="Description">
<ArgTableRow arg="enabled" typ="bool">Whether the router answers MAC pings. It is also needed for the router's own MAC pings: with the server disabled, they fail with the status `unknown interface`. ARP ping does not depend on this setting. Default: yes.</ArgTableRow>
</ArgTable>
