---
type: Reference
title: "/caps-man/radio"
description: "RouterOS directory reference for /caps-man/radio"
timestamp: '2026-10-06'
status: active
tags: [routeros, mikrotik, manual, cli-reference]
resource: https://manual.mikrotik.com/docs/cli-reference/caps-man/radio.md
sources:
  - resource: https://manual.mikrotik.com/docs/cli-reference/caps-man/radio.md
---

-----------

## caps-man/radio 
**Package:** wireless-rep
**Type:** Directory

<ArgTable c1="Flag" c2="Name" c3="Description">
<ArgTableRow arg="L" typ="local"></ArgTableRow>
<ArgTableRow arg="P" typ="provisioned"></ArgTableRow>
</ArgTable>

<ArgTable c1="Read-only Argument" c2="Type" c3="Description">
<ArgTableRow arg="radio-mac" typ="macAddr"></ArgTableRow>
<ArgTableRow arg="remote-cap-name" typ="string"></ArgTableRow>
<ArgTableRow arg="remote-cap-identity" typ="string"></ArgTableRow>
<ArgTableRow arg="interface" typ="iface_enum"></ArgTableRow>
</ArgTable>
