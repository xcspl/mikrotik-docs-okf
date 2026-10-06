---
type: Reference
title: "/ip/ssh/import-host-key"
description: "Import and replace the private RSA/Ed25519 key from a specified file"
timestamp: '2026-10-06'
status: active
tags: [routeros, mikrotik, manual, cli-reference]
resource: https://manual.mikrotik.com/docs/cli-reference/ip/ssh/import-host-key.md
sources:
  - resource: https://manual.mikrotik.com/docs/cli-reference/ip/ssh/import-host-key.md
---

-----------

## ip/ssh/import-host-key 
**Type:** Command

Import and replace the private RSA/Ed25519 key from a specified file

:::info
The private key is supported in PEM or PKCS#8 format.
:::

<ArgTable c1="Argument" c2="Type" c3="Description">
<ArgTableRow arg="private-key-file" typ="file">Name of the private RSA/Ed25519 key file in PEM or PKCS#8 format.</ArgTableRow>
<ArgTableRow arg="passphrase" typ="string">Private key passphrase.</ArgTableRow>
</ArgTable>
