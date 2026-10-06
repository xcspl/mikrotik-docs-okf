---
type: Reference
title: "/system/backup/cloud/remove-file"
description: "Deletes the backup from the cloud server and frees the slot of this device. Give the backup by its number in the list, for example remove-file number=0"
timestamp: '2026-10-06'
status: active
tags: [routeros, mikrotik, manual, cli-reference]
resource: https://manual.mikrotik.com/docs/cli-reference/system/backup/cloud/remove-file.md
sources:
  - resource: https://manual.mikrotik.com/docs/cli-reference/system/backup/cloud/remove-file.md
---

-----------

## system/backup/cloud/remove-file 
**Type:** Command

Deletes the backup from the cloud server and frees the slot of this device. Give the backup by its number in the list, for example `remove-file number=0`.

<ArgTable c1="Read-only Argument" c2="Type" c3="Description">
<ArgTableRow arg="status" typ="string">Progress of the command: `working...` while it runs, `finished` when it is done, or the error message, for example from the cloud server.</ArgTableRow>
</ArgTable>
