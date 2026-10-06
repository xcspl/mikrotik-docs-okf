---
type: Reference
title: "/caps-man/remote-cap"
description: "RouterOS directory reference for /caps-man/remote-cap"
timestamp: '2026-10-06'
status: active
tags: [routeros, mikrotik, manual, cli-reference]
resource: https://manual.mikrotik.com/docs/cli-reference/caps-man/remote-cap.md
sources:
  - resource: https://manual.mikrotik.com/docs/cli-reference/caps-man/remote-cap.md
---

-----------

## caps-man/remote-cap 
**Package:** wireless-rep
**Type:** Directory

<ArgTable c1="Read-only Argument" c2="Type" c3="Description">
<ArgTableRow arg="state" typ="string"></ArgTableRow>
<ArgTableRow arg="name" typ="string"></ArgTableRow>
<ArgTableRow arg="radios" typ="num"></ArgTableRow>
<ArgTableRow arg="address" typ="super { address: alt { ip-address: ip6Addr
, mac-address: macAddr
 }
, [port] /num
 }"></ArgTableRow>
<ArgTableRow arg="board" typ="string"></ArgTableRow>
<ArgTableRow arg="serial" typ="string"></ArgTableRow>
<ArgTableRow arg="base-mac" typ="string"></ArgTableRow>
<ArgTableRow arg="version" typ="string"></ArgTableRow>
<ArgTableRow arg="identity" typ="string"></ArgTableRow>
</ArgTable>
