---
type: Reference
title: "/system/ntp/key"
description: "Symmetric keys for NTP authentication, selected by their key ID in /system/ntp/client/servers and /system/ntp/server. The key value is sensitive: it is not shown in print or saved in export output. See the NTP guide"
timestamp: '2026-10-06'
status: active
tags: [routeros, mikrotik, manual, cli-reference]
resource: https://manual.mikrotik.com/docs/cli-reference/system/ntp/key.md
sources:
  - resource: https://manual.mikrotik.com/docs/cli-reference/system/ntp/key.md
---

-----------

## system/ntp/key 
**Type:** Directory

Symmetric keys for NTP authentication, selected by their key ID in [`/system/ntp/client/servers`](https://manual.mikrotik.com/docs/cli-reference/system/ntp/client/servers) and [`/system/ntp/server`](https://manual.mikrotik.com/docs/cli-reference/system/ntp/server). The key value is sensitive: it is not shown in `print` or saved in `export` output. See the [NTP](https://manual.mikrotik.com/docs/system-information-and-utilities/ntp) guide.

<ArgTable c1="Argument" c2="Type" c3="Description">
<ArgTableRow arg="key-id" typ="num" mandatory="1">Key identifier, referenced by `auth-key` in the client and server configuration.</ArgTableRow>
<ArgTableRow arg="key-val" typ="string" mandatory="1">The shared secret. Not included in `export` output.</ArgTableRow>
</ArgTable>
