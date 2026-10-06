---
type: Reference
title: "/tool/mac-server"
description: "MAC Telnet server settings. The MAC server lets devices on the same layer-2 segment reach the router by its MAC address, without IP configuration: MAC Telnet (this menu), MAC WinBox (/tool/mac-server/mac-winbox) and"
timestamp: '2026-10-06'
status: active
tags: [routeros, mikrotik, manual, cli-reference]
resource: https://manual.mikrotik.com/docs/cli-reference/tool/mac-server.md
sources:
  - resource: https://manual.mikrotik.com/docs/cli-reference/tool/mac-server.md
---

-----------

## tool/mac-server 
**Type:** Settings Directory

MAC Telnet server settings. The MAC server lets devices on the same layer-2 segment reach the router by its MAC address, without IP configuration: MAC Telnet (this menu), MAC WinBox ([`/tool/mac-server/mac-winbox`](https://manual.mikrotik.com/docs/cli-reference/tool/mac-winbox)) and MAC ping ([`/tool/mac-server/ping`](https://manual.mikrotik.com/docs/cli-reference/tool/ping)). Open MAC Telnet sessions are listed in [`/tool/mac-server/sessions`](https://manual.mikrotik.com/docs/cli-reference/tool/sessions). The IP firewall does not stop MAC access; limit it with `allowed-interface-list`. For examples, see [MAC server](https://manual.mikrotik.com/management-tools/mac-server).

<ArgTable c1="Argument" c2="Type" c3="Description">
<ArgTableRow arg="allowed-interface-list" typ="enum">Interface list on which the router accepts MAC Telnet connections. A bridge in the list also allows connections that arrive through its ports; a bridge port alone in the list does not. `none`, or a list without members, turns MAC Telnet off. A change applies to the next connection at once; open sessions stay. The default configuration sets `LAN`. Default: all.</ArgTableRow>
</ArgTable>
