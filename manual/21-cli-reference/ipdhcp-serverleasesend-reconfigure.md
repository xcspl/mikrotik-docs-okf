---
type: Reference
title: "/ip/dhcp-server/lease/send-reconfigure"
description: "Sends a Reconfigure (FORCERENEW) message to the client of the lease, which makes the client renew its lease immediately. It works only for clients that got a reconfigure key, which requires use-reconfigure=yes on the"
timestamp: '2026-10-06'
status: active
tags: [routeros, mikrotik, manual, cli-reference]
resource: https://manual.mikrotik.com/docs/cli-reference/ip/dhcp-server/lease/send-reconfigure.md
sources:
  - resource: https://manual.mikrotik.com/docs/cli-reference/ip/dhcp-server/lease/send-reconfigure.md
---

-----------

## ip/dhcp-server/lease/send-reconfigure 
**Type:** Command

Sends a Reconfigure (FORCERENEW) message to the client of the lease, which makes the client renew its lease immediately. It works only for clients that got a reconfigure key, which requires `use-reconfigure=yes` on the server and a client that asks for the key, for example a RouterOS DHCP client with `allow-reconfigure=yes`.
