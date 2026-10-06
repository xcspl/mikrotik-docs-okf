---
type: Reference
title: "/system/backup/cloud"
description: "Backup of this device stored on the MikroTik cloud server. Each device has one slot. Every command in this menu, including print, connects to cloud2.mikrotik.com. For examples, see Cloud backup"
timestamp: '2026-10-06'
status: active
tags: [routeros, mikrotik, manual, cli-reference]
resource: https://manual.mikrotik.com/docs/cli-reference/system/backup/cloud.md
sources:
  - resource: https://manual.mikrotik.com/docs/cli-reference/system/backup/cloud.md
---

-----------

## system/backup/cloud 
**Type:** Directory

Backup of this device stored on the MikroTik cloud server. Each device has one slot. Every command in this menu, including `print`, connects to `cloud2.mikrotik.com`. For examples, see [Cloud backup](https://manual.mikrotik.com/network-management/cloud/cloud-backup).

<ArgTable c1="Read-only Argument" c2="Type" c3="Description">
<ArgTableRow arg="name" typ="string">Name of the backup, set with `name` in `upload-file`. `download-file` saves the backup as `<name>.backup` unless `dst-file` is given.</ArgTableRow>
<ArgTableRow arg="size" typ="num">Size of the encrypted backup file.</ArgTableRow>
<ArgTableRow arg="ros-version" typ="string">RouterOS version that created the backup.</ArgTableRow>
<ArgTableRow arg="date" typ="date">Time of the upload.</ArgTableRow>
<ArgTableRow arg="status" typ="string">State of the stored backup. `ok` when the backup can be downloaded.</ArgTableRow>
<ArgTableRow arg="secret-download-key" typ="string">Key that downloads this backup on any router, with `download-file secret-download-key=<key>`. Replacing the backup generates a new key. Anyone who has the key can download the file, but cannot read it without the backup password.</ArgTableRow>
</ArgTable>
