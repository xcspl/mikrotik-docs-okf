---
type: Reference
title: "/ip/hotspot/setup"
description: "RouterOS command reference for /ip/hotspot/setup"
timestamp: '2026-10-06'
status: active
tags: [routeros, mikrotik, manual, cli-reference]
resource: https://manual.mikrotik.com/docs/cli-reference/ip/hotspot/setup.md
sources:
  - resource: https://manual.mikrotik.com/docs/cli-reference/ip/hotspot/setup.md
---

-----------

## ip/hotspot/setup 
**Type:** Command

<ArgTable c1="Read-only Argument" c2="Type" c3="Description">
<ArgTableRow arg="interface" typ="alt { interface1: iface_enum
, interface2: iface_enum
 }"></ArgTableRow>
<ArgTableRow arg="address" typ="composite { address: ipAddr
, netmask: num
 }"></ArgTableRow>
<ArgTableRow arg="masq" typ="bool"></ArgTableRow>
<ArgTableRow arg="pool" typ="multi { range: composite { min: ipAddr
, max: ipAddr
 }
 }"></ArgTableRow>
<ArgTableRow arg="ssl-cert" typ="enum (import-other-certificate | none) { import-other-certificate:0, none:0xffffffff }"></ArgTableRow>
<ArgTableRow arg="passphrase" typ="string"></ArgTableRow>
<ArgTableRow arg="smtp-server" typ="ipAddr"></ArgTableRow>
<ArgTableRow arg="use-dnscache" typ="bool"></ArgTableRow>
<ArgTableRow arg="dns-server" typ="multi { address: ipAddr
 }"></ArgTableRow>
<ArgTableRow arg="dns-name" typ="string"></ArgTableRow>
<ArgTableRow arg="username" typ="string"></ArgTableRow>
<ArgTableRow arg="password" typ="string"></ArgTableRow>
</ArgTable>
