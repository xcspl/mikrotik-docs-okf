---
type: Reference
title: "/tool/mac-server/sessions"
description: "Open MAC Telnet sessions to this router. MAC WinBox connections are not listed. For examples, see MAC server"
timestamp: '2026-10-06'
status: active
tags: [routeros, mikrotik, manual, cli-reference]
resource: https://manual.mikrotik.com/docs/cli-reference/tool/mac-server/sessions.md
sources:
  - resource: https://manual.mikrotik.com/docs/cli-reference/tool/mac-server/sessions.md
---

-----------

## tool/mac-server/sessions 
**Type:** Directory

Open MAC Telnet sessions to this router. MAC WinBox connections are not listed. For examples, see [MAC server](https://manual.mikrotik.com/docs/management-tools/mac-server).

<ArgTable c1="Argument" c2="Type" c3="Description">
<ArgTableRow arg="interface" typ="iface_enum">Interface the session arrived on.</ArgTableRow>
<ArgTableRow arg="src-address" typ="macAddr">MAC address of the client.</ArgTableRow>
<ArgTableRow arg="uptime" typ="time">How long the session has been open.</ArgTableRow>
</ArgTable>
