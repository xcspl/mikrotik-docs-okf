---
type: Reference
title: "/ipv6/dhcp-server/binding/send-reconfigure"
description: "Sends a Reconfigure message to the client of the binding, which makes the client renew immediately. Requires use-reconfigure=yes on the server and a client that accepts Reconfigure messages, for example a RouterOS"
timestamp: '2026-10-06'
status: active
tags: [routeros, mikrotik, manual, cli-reference]
resource: https://manual.mikrotik.com/docs/cli-reference/ipv6/dhcp-server/binding/send-reconfigure.md
sources:
  - resource: https://manual.mikrotik.com/docs/cli-reference/ipv6/dhcp-server/binding/send-reconfigure.md
---

-----------

## ipv6/dhcp-server/binding/send-reconfigure 
**Type:** Command

Sends a Reconfigure message to the client of the binding, which makes the client renew immediately. Requires `use-reconfigure=yes` on the server and a client that accepts Reconfigure messages, for example a RouterOS DHCPv6 client with `allow-reconfigure=yes`.
