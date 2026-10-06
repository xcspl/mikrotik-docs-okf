---
type: Reference
title: "/disk/settings"
description: "RouterOS settings reference for /disk/settings"
timestamp: '2026-10-06'
status: active
tags: [routeros, mikrotik, manual, cli-reference]
resource: https://manual.mikrotik.com/docs/cli-reference/disk/settings.md
sources:
  - resource: https://manual.mikrotik.com/docs/cli-reference/disk/settings.md
---

-----------

## disk/settings 
**Conditions:** !smips
**Type:** Settings Directory

<ArgTable c1="Argument" c2="Type" c3="Description">
<ArgTableRow arg="default-mount-point-template" typ="string">Mount point template that new disks and partitions get in place of their own `mount-point-template` when they are added. The template variables are the same as on a disk item (`[slot]`, `[model]`, `[serial]`, `[fw-version]`, `[fs-label]`, `[fs-uuid]`, `[fs]`). Default: [slot].</ArgTableRow>
<ArgTableRow arg="auto-smb-sharing" typ="bool">Whether a new disk or partition automatically gets an SMB share (see the SMB page). New items created by a later format get the share as well, and so do new `tmpfs` folders. The default configuration of some routers, for example the hAP ax², sets it to `yes`, so new disks and folders are shared on the LAN. Default: no.</ArgTableRow>
<ArgTableRow arg="auto-smb-user" typ="enum">Default user of the automatic SMB share created by `auto-smb-sharing=yes`. Default: guest.</ArgTableRow>
<ArgTableRow arg="auto-media-sharing" typ="bool">Whether a new disk or partition, including a new `tmpfs` folder, is automatically added to the DLNA media server (`/ip/media`). The default configuration of some routers, for example the hAP ax², sets it to `yes`. Default: no.</ArgTableRow>
<ArgTableRow arg="auto-media-interface" typ="iface_enum { none }">Interface used in the dynamic `/ip/media` entry created for a new disk when `auto-media-sharing=yes`. The default configuration of some routers, for example the hAP ax², sets it to `bridge`. Default: none.</ArgTableRow>
</ArgTable>
