---
type: Reference
title: "/ip/ssh/export-host-key"
description: "Export public and private RSA/Ed25519 keys to files"
timestamp: '2026-10-06'
status: active
tags: [routeros, mikrotik, manual, cli-reference]
resource: https://manual.mikrotik.com/docs/cli-reference/ip/ssh/export-host-key.md
sources:
  - resource: https://manual.mikrotik.com/docs/cli-reference/ip/ssh/export-host-key.md
---

-----------

## ip/ssh/export-host-key 
**Type:** Command

Export public and private RSA/Ed25519 keys to files.

:::info
Host keys are exported in PKCS#8 format.

Exporting the SSH host key requires "sensitive" user policy.
:::

<ArgTable c1="Argument" c2="Type" c3="Description">
<ArgTableRow arg="key-file-prefix" typ="string">Prefix for generated files. For example, prefix 'my' generates files 'my_rsa', 'my_rsa.pub'. Host keys are exported in PKCS#8 format.</ArgTableRow>
<ArgTableRow arg="passphrase" typ="string">Private key passphrase.</ArgTableRow>
</ArgTable>
