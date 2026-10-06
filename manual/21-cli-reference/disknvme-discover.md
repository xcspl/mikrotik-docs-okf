---
type: Reference
title: "/disk/nvme-discover"
description: "RouterOS command reference for /disk/nvme-discover"
timestamp: '2026-10-06'
status: active
tags: [routeros, mikrotik, manual, cli-reference]
resource: https://manual.mikrotik.com/docs/cli-reference/disk/nvme-discover.md
sources:
  - resource: https://manual.mikrotik.com/docs/cli-reference/disk/nvme-discover.md
---

-----------

## disk/nvme-discover 
**Conditions:** !smips
**Syscap:** storage
**Type:** Command

<ArgTable c1="Argument" c2="Type" c3="Description">
<ArgTableRow arg="address" typ="ipAddr">IP address of the NVMe over TCP controller.</ArgTableRow>
<ArgTableRow arg="port" typ="num">TCP port of the controller's discovery service. Default: 4420.</ArgTableRow>
<ArgTableRow arg="host-name" typ="string">Host NQN this router presents to the controller, used for identification and host-based access control.</ArgTableRow>
</ArgTable>

<ArgTable c1="Read-only Argument" c2="Type" c3="Description">
<ArgTableRow arg="nqn" typ="string">NVMe Qualified Name of a subsystem the controller exposes.</ArgTableRow>
</ArgTable>
