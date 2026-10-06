---
type: Reference
title: "/user/ssh-keys/private"
description: "Private SSH keys that identify the router in outgoing SSH connections to other devices, for example with /system/ssh or /tool/fetch. All properties are read-only; keys are added with /user/ssh-keys/private/import"
timestamp: '2026-10-06'
status: active
tags: [routeros, mikrotik, manual, cli-reference]
resource: https://manual.mikrotik.com/docs/cli-reference/user/ssh-keys/private.md
sources:
  - resource: https://manual.mikrotik.com/docs/cli-reference/user/ssh-keys/private.md
---

-----------

## user/ssh-keys/private 
**Type:** Directory

Private SSH keys that identify the router in outgoing SSH connections to other devices, for example with [`/system/ssh`](https://manual.mikrotik.com/docs/system/ssh) or [`/tool/fetch`](https://manual.mikrotik.com/docs/tool/fetch). All properties are read-only; keys are added with [`/user/ssh-keys/private/import`](https://manual.mikrotik.com/docs/cli-reference/user/ssh-keys/import). See [User](https://manual.mikrotik.com/authentication-authorization-accounting/user) for the full guide.

<ArgTable c1="Read-only Argument" c2="Type" c3="Description">
<ArgTableRow arg="user" typ="enum">System user that owns the key.</ArgTableRow>
<ArgTableRow arg="key-type" typ="enum (rsa | ed25519)">Type of the key: `rsa` or `ed25519`.</ArgTableRow>
<ArgTableRow arg="bits" typ="num">Key length in bits.</ArgTableRow>
<ArgTableRow arg="info" typ="string">Free-text label for the key.</ArgTableRow>
</ArgTable>
