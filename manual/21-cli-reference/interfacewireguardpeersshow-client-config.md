---
type: Reference
title: "/interface/wireguard/peers/show-client-config"
description: "RouterOS command reference for /interface/wireguard/peers/show-client-config"
timestamp: '2026-10-06'
status: active
tags: [routeros, mikrotik, manual, cli-reference]
resource: https://manual.mikrotik.com/docs/cli-reference/interface/wireguard/peers/show-client-config.md
sources:
  - resource: https://manual.mikrotik.com/docs/cli-reference/interface/wireguard/peers/show-client-config.md
---

-----------

## interface/wireguard/peers/show-client-config 
**Type:** Command

<ArgTable c1="Argument" c2="Type" c3="Description">
<ArgTableRow arg="file" typ="file">Name of the file to save the client configuration to.</ArgTableRow>
</ArgTable>

<ArgTable c1="Read-only Argument" c2="Type" c3="Description">
<ArgTableRow arg="conf" typ="string">The client configuration text.</ArgTableRow>
<ArgTableRow arg="qr" typ="pic">QR code generated from the client configuration for easier peer setup on a mobile device.</ArgTableRow>
</ArgTable>
