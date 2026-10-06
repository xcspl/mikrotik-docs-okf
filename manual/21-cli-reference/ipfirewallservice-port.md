---
type: Reference
title: "/ip/firewall/service-port"
description: "RouterOS directory reference for /ip/firewall/service-port"
timestamp: '2026-10-06'
status: active
tags: [routeros, mikrotik, manual, cli-reference]
resource: https://manual.mikrotik.com/docs/cli-reference/ip/firewall/service-port.md
sources:
  - resource: https://manual.mikrotik.com/docs/cli-reference/ip/firewall/service-port.md
---

-----------

## ip/firewall/service-port 
**Type:** Directory

<ArgTable c1="Flag" c2="Name" c3="Description">
<ArgTableRow arg="X" typ="disabled">disabled</ArgTableRow>
<ArgTableRow arg="I" typ="invalid">invalid</ArgTableRow>
</ArgTable>

<ArgTable c1="Argument" c2="Type" c3="Description">
<ArgTableRow arg="ports" typ="multi { port: num [0 .. 65535]
 }">Port numbers used by the service.</ArgTableRow>
<ArgTableRow arg="sip-direct-media" typ="bool">Whether SIP direct media is enabled.</ArgTableRow>
<ArgTableRow arg="sip-timeout" typ="time">SIP timeout value.</ArgTableRow>
</ArgTable>

<ArgTable c1="Read-only Argument" c2="Type" c3="Description">
<ArgTableRow arg="name" typ="string">Name of the service.</ArgTableRow>
</ArgTable>
