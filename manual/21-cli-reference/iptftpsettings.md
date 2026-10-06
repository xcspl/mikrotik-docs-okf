---
type: Reference
title: "/ip/tftp/settings"
description: "Settings of the TFTP server. See TFTP"
timestamp: '2026-10-06'
status: active
tags: [routeros, mikrotik, manual, cli-reference]
resource: https://manual.mikrotik.com/docs/cli-reference/ip/tftp/settings.md
sources:
  - resource: https://manual.mikrotik.com/docs/cli-reference/ip/tftp/settings.md
---

-----------

## ip/tftp/settings 
**Type:** Settings Directory

Settings of the TFTP server. See [TFTP](https://manual.mikrotik.com/docs/system-information-and-utilities/tftp).

<ArgTable c1="Argument" c2="Type" c3="Description">
<ArgTableRow arg="max-block-size" typ="enum (512 | 1454 | 4096 | 8192) { 512:512, 1454:1454, 4096:4096, 8192:8192 }">Largest block size the router agrees to when a client asks for one (the `blksize` option); a client that asks for more gets this size. Clients that do not ask use 512 bytes. Values: `512`, `1454`, `4096`, `8192`. Default: 4096.</ArgTableRow>
<ArgTableRow arg="vrf" typ="enum">VRF the TFTP server listens in. Default: main.</ArgTableRow>
</ArgTable>
