---
type: Reference
title: "/system/routerboard/usb"
description: "RouterOS settings reference for /system/routerboard/usb"
timestamp: '2026-10-06'
status: active
tags: [routeros, mikrotik, manual, cli-reference]
resource: https://manual.mikrotik.com/docs/cli-reference/system/routerboard/usb.md
sources:
  - resource: https://manual.mikrotik.com/docs/cli-reference/system/routerboard/usb.md
---

-----------

## system/routerboard/usb 
**Conditions:** !i386, !i386, !mipsel, !powerpc
**Type:** Settings Directory

<ArgTable c1="Argument" c2="Type" c3="Description">
<ArgTableRow arg="type" typ="enum (USB-type-A | mini-PCIe | auto)"></ArgTableRow>
<ArgTableRow arg="usb-mode" typ="enum (automatic | force-host) { automatic:0, force-host:1 }"></ArgTableRow>
</ArgTable>

<ArgTable c1="Read-only Argument" c2="Type" c3="Description">
<ArgTableRow arg="auto-type" typ="enum (USB-type-A | mini-PCIe)"></ArgTableRow>
<ArgTableRow arg="bootstrap" typ="enum (host-mode | device-mode) { host-mode:0, device-mode:1 }"></ArgTableRow>
</ArgTable>
