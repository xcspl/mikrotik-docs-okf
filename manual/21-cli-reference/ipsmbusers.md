---
type: Reference
title: "/ip/smb/users"
description: "RouterOS directory reference for /ip/smb/users"
timestamp: '2026-10-06'
status: active
tags: [routeros, mikrotik, manual, cli-reference]
resource: https://manual.mikrotik.com/docs/cli-reference/ip/smb/users.md
sources:
  - resource: https://manual.mikrotik.com/docs/cli-reference/ip/smb/users.md
---

-----------

## ip/smb/users 
**Conditions:** !smips
**Type:** Directory

<ArgTable c1="Flag" c2="Name" c3="Description">
<ArgTableRow arg="D" typ="dynamic">The entry is created automatically.</ArgTableRow>
<ArgTableRow arg="X" typ="disabled">The user is disabled and cannot log in.</ArgTableRow>
<ArgTableRow arg="*" typ="default">The entry is a default entry created by the system.</ArgTableRow>
<ArgTableRow arg="r" typ="read-only">The user has read-only access to the shares.</ArgTableRow>
</ArgTable>

<ArgTable c1="Argument" c2="Type" c3="Description">
<ArgTableRow arg="name" typ="string" mandatory="1">Login name of the SMB service user.</ArgTableRow>
<ArgTableRow arg="password" typ="string">Password of the SMB user.</ArgTableRow>
<ArgTableRow arg="read-only" typ="bool">Whether the user has read-only access to the shares. Default: yes.</ArgTableRow>
</ArgTable>
