---
type: Reference
title: "/tool/mac-server/mac-winbox"
description: "MAC WinBox server settings: on which interfaces WinBox can connect to the router by its MAC address. MAC Telnet has its own setting in /tool/mac-server. For examples, see MAC server"
timestamp: '2026-10-06'
status: active
tags: [routeros, mikrotik, manual, cli-reference]
resource: https://manual.mikrotik.com/docs/cli-reference/tool/mac-server/mac-winbox.md
sources:
  - resource: https://manual.mikrotik.com/docs/cli-reference/tool/mac-server/mac-winbox.md
---

-----------

## tool/mac-server/mac-winbox 
**Type:** Settings Directory

MAC WinBox server settings: on which interfaces WinBox can connect to the router by its MAC address. MAC Telnet has its own setting in [`/tool/mac-server`](https://manual.mikrotik.com/docs/cli-reference/tool/mac-server/). For examples, see [MAC server](https://manual.mikrotik.com/docs/management-tools/mac-server).

<ArgTable c1="Argument" c2="Type" c3="Description">
<ArgTableRow arg="allowed-interface-list" typ="enum">Interface list on which the router accepts MAC WinBox connections, set the same way as for MAC Telnet in [`/tool/mac-server`](https://manual.mikrotik.com/docs/cli-reference/tool/mac-server/): put the bridge in the list, not its ports. `none` turns MAC WinBox off. The default configuration sets `LAN`. Default: all.</ArgTableRow>
</ArgTable>
