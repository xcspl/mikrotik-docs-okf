---
type: Reference
title: "/system/backup/save"
description: "Command saves the configuration in binary backup file"
timestamp: '2026-10-06'
status: active
tags: [routeros, mikrotik, manual, cli-reference]
resource: https://manual.mikrotik.com/docs/cli-reference/system/backup/save.md
sources:
  - resource: https://manual.mikrotik.com/docs/cli-reference/system/backup/save.md
---

-----------

## system/backup/save 
**Type:** Command

Command saves the configuration in binary [backup file](https://manual.mikrotik.com/docs/getting-started/configuration-management/backup.md).

<ArgTable c1="Argument" c2="Type" c3="Description">
<ArgTableRow arg="name" typ="file">The filename for the backup file.</ArgTableRow>
<ArgTableRow arg="password" typ="string">Password for the encrypted backup file. Since RouterOS v6.43, without a provided password, the backup file is unencrypted.</ArgTableRow>
<ArgTableRow arg="dont-encrypt" typ="bool">Disable backup file encryption. Since RouterOS v6.43, without a provided password, the backup file is unencrypted.</ArgTableRow>
<ArgTableRow arg="encryption" typ="enum (aes-sha256 | rc4) { aes-sha256:0, rc4:1 }">The encryption algorithm to use for encrypting the backup file. `rc4` is not a secure encryption method and is only available for compatibility with older RouterOS versions.</ArgTableRow>
</ArgTable>
