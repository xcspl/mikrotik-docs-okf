---
type: Reference
title: "/system/identity"
description: "The name of the router. For where it appears and examples, see Identity"
timestamp: '2026-10-06'
status: active
tags: [routeros, mikrotik, manual, cli-reference]
resource: https://manual.mikrotik.com/docs/cli-reference/system/identity.md
sources:
  - resource: https://manual.mikrotik.com/docs/cli-reference/system/identity.md
---

-----------

## system/identity 
**Type:** Settings Directory

The name of the router. For where it appears and examples, see [Identity](https://manual.mikrotik.com/docs/system-information-and-utilities/identity).

<ArgTable c1="Argument" c2="Type" c3="Description">
<ArgTableRow arg="name" typ="string">Name of the router, up to 64 characters; spaces and other characters are allowed, a longer name fails with `could not change identity: too long`. It appears in the CLI prompt and in WinBox, in neighbor discovery, as the SNMP `sysName`, as the host name the DHCP client sends, and as the default SSID of legacy wireless interfaces. SNMP can set it with a community that has write access. Default: MikroTik.</ArgTableRow>
</ArgTable>
