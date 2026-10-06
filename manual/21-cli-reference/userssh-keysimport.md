---
type: Reference
title: "/user/ssh-keys/import"
description: "Imports a public SSH key from a file in the router's root directory and assigns it to a user. Accepted formats: OpenSSH single-line, PKCS#1 PEM ('BEGIN RSA PUBLIC KEY') and PKCS#8/SPKI PEM ('BEGIN PUBLIC KEY'). See"
timestamp: '2026-10-06'
status: active
tags: [routeros, mikrotik, manual, cli-reference]
resource: https://manual.mikrotik.com/docs/cli-reference/user/ssh-keys/import.md
sources:
  - resource: https://manual.mikrotik.com/docs/cli-reference/user/ssh-keys/import.md
---

-----------

## user/ssh-keys/import 
**Type:** Command

Imports a public SSH key from a file in the router's root directory and assigns it to a user. Accepted formats: OpenSSH single-line, PKCS#1 PEM ("BEGIN RSA PUBLIC KEY") and PKCS#8/SPKI PEM ("BEGIN PUBLIC KEY"). See [User](https://manual.mikrotik.com/docs/authentication-authorization-accounting/user) for the full guide.

<ArgTable c1="Argument" c2="Type" c3="Description">
<ArgTableRow arg="public-key-file" typ="file">Name of the key file in the router's root directory.</ArgTableRow>
<ArgTableRow arg="user" typ="enum">System user to assign the key to.</ArgTableRow>
<ArgTableRow arg="info" typ="string">Free-text label for the key.</ArgTableRow>
</ArgTable>
