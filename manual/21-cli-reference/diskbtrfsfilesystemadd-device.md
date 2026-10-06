---
type: Reference
title: "/disk/btrfs/filesystem/add-device"
description: "RouterOS command reference for /disk/btrfs/filesystem/add-device"
timestamp: '2026-10-06'
status: active
tags: [routeros, mikrotik, manual, cli-reference]
resource: https://manual.mikrotik.com/docs/cli-reference/disk/btrfs/filesystem/add-device.md
sources:
  - resource: https://manual.mikrotik.com/docs/cli-reference/disk/btrfs/filesystem/add-device.md
---

-----------

## disk/btrfs/filesystem/add-device 
**Conditions:** !smips
**Syscap:** storage
**Type:** Command

<ArgTable c1="Argument" c2="Type" c3="Description">
<ArgTableRow arg="device" typ="enum">Disk slot to add to the Btrfs file system, for example `nvme9`. After adding a device, run [`balance-start`](https://manual.mikrotik.com/docs/cli-reference/disk/btrfs/filesystem/balance-start) with the desired profiles (for example `data-profile=raid1`) to actually use it for storage redundancy; otherwise the device is only listed under `devs`.</ArgTableRow>
</ArgTable>
