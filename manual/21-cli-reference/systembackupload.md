---
type: Reference
title: "/system/backup/load"
description: "Command loads the configuration from backup files"
timestamp: '2026-10-06'
status: active
tags: [routeros, mikrotik, manual, cli-reference]
resource: https://manual.mikrotik.com/docs/cli-reference/system/backup/load.md
sources:
  - resource: https://manual.mikrotik.com/docs/cli-reference/system/backup/load.md
---

-----------

## system/backup/load 
**Type:** Command

Command loads the configuration from [backup files](https://manual.mikrotik.com/docs/getting-started/configuration-management/backup.md).

<ArgTable c1="Argument" c2="Type" c3="Description">
<ArgTableRow arg="name" typ="file">File name for the backup file.</ArgTableRow>
<ArgTableRow arg="password" typ="string">Password for the encrypted backup file.</ArgTableRow>
<ArgTableRow arg="force-v6-to-v7-configuration-upgrade" typ="bool">This setting after loading the config (if backup has the ROSv6 config) is forcing to run configuration conversion to v7.</ArgTableRow>
</ArgTable>
