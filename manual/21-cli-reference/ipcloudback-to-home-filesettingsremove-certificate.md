---
type: Reference
title: "/ip/cloud/back-to-home-file/settings/remove-certificate"
description: "Deletes the File Share certificate from /certificate. It works only when no share exists; otherwise, it fails with cannot remove certificate while file shares active. The next share requests a new certificate. See"
timestamp: '2026-10-06'
status: active
tags: [routeros, mikrotik, manual, cli-reference]
resource: https://manual.mikrotik.com/docs/cli-reference/ip/cloud/back-to-home-file/settings/remove-certificate.md
sources:
  - resource: https://manual.mikrotik.com/docs/cli-reference/ip/cloud/back-to-home-file/settings/remove-certificate.md
---

-----------

## ip/cloud/back-to-home-file/settings/remove-certificate 
**Syscap:** cloud-vpn
**Type:** Command

Deletes the File Share certificate from `/certificate`. It works only when no share exists; otherwise, it fails with `cannot remove certificate while file shares active`. The next share requests a new certificate. See [Stop File Share](https://manual.mikrotik.com/docs/network-management/cloud/file-share#stop-file-share).
