---
type: Reference
title: "/user/ssh-keys/private/import"
description: "Imports a private SSH key from a file in the router's root directory. Accepted formats: PKCS#1 PEM RSA ('BEGIN RSA PRIVATE KEY'), PKCS#8 ('BEGIN PRIVATE KEY') and encrypted PKCS#8 ('BEGIN ENCRYPTED PRIVATE KEY',"
timestamp: '2026-10-06'
status: active
tags: [routeros, mikrotik, manual, cli-reference]
resource: https://manual.mikrotik.com/docs/cli-reference/user/ssh-keys/private/import.md
sources:
  - resource: https://manual.mikrotik.com/docs/cli-reference/user/ssh-keys/private/import.md
---

-----------

## user/ssh-keys/private/import 
**Type:** Command

Imports a private SSH key from a file in the router's root directory. Accepted formats: PKCS#1 PEM RSA ("BEGIN RSA PRIVATE KEY"), PKCS#8 ("BEGIN PRIVATE KEY") and encrypted PKCS#8 ("BEGIN ENCRYPTED PRIVATE KEY", requires `passphrase`). OpenSSH-format private keys ("BEGIN OPENSSH PRIVATE KEY") are rejected. See [User](https://manual.mikrotik.com/docs/authentication-authorization-accounting/user) for the full guide.

<ArgTable c1="Argument" c2="Type" c3="Description">
<ArgTableRow arg="private-key-file" typ="file">Name of the key file in the router's root directory.</ArgTableRow>
<ArgTableRow arg="user" typ="enum">System user that owns the key.</ArgTableRow>
<ArgTableRow arg="passphrase" typ="string">Passphrase of an encrypted key file.</ArgTableRow>
<ArgTableRow arg="info" typ="string">Free-text label for the key.</ArgTableRow>
</ArgTable>
