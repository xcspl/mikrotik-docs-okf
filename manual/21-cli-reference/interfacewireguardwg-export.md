---
type: Reference
title: "/interface/wireguard/wg-export"
description: "Export the selected WireGuard interface and its peers in standard WireGuard configuration format. Select the interface with [find name=...]. The export does not include interface IP addresses, routes or firewall"
timestamp: '2026-10-06'
status: active
tags: [routeros, mikrotik, manual, cli-reference]
resource: https://manual.mikrotik.com/docs/cli-reference/interface/wireguard/wg-export.md
sources:
  - resource: https://manual.mikrotik.com/docs/cli-reference/interface/wireguard/wg-export.md
---

-----------

## interface/wireguard/wg-export 
**Type:** Command

Export the selected WireGuard interface and its peers in standard WireGuard configuration format. Select the interface with `[find name=...]`. The export does not include interface IP addresses, routes or firewall rules. For an executable RouterOS script, use the regular `/interface/wireguard/export` command. See [WireGuard](https://manual.mikrotik.com/docs/virtual-private-networks/wireguard).

<ArgTable c1="Argument" c2="Type" c3="Description">
<ArgTableRow arg="file" typ="file">Name of the file to export the selected WireGuard interface and its peers to. The file contains `[Interface]` and `[Peer]` sections and the private key; store it securely.</ArgTableRow>
</ArgTable>
