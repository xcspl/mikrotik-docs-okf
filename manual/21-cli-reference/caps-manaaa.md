---
type: Reference
title: "/caps-man/aaa"
description: "RouterOS settings reference for /caps-man/aaa"
timestamp: '2026-10-06'
status: active
tags: [routeros, mikrotik, manual, cli-reference]
resource: https://manual.mikrotik.com/docs/cli-reference/caps-man/aaa.md
sources:
  - resource: https://manual.mikrotik.com/docs/cli-reference/caps-man/aaa.md
---

-----------

## caps-man/aaa 
**Package:** wireless-rep
**Type:** Settings Directory

<ArgTable c1="Argument" c2="Type" c3="Description">
<ArgTableRow arg="mac-format" typ="string"></ArgTableRow>
<ArgTableRow arg="mac-mode" typ="enum (as-username | as-username-and-password) { as-username:0, as-username-and-password:1 }"></ArgTableRow>
<ArgTableRow arg="mac-caching" typ="alt { mac-caching-disable: enum (disabled) { disabled:0 }
, mac-caching-time: time
 }"></ArgTableRow>
<ArgTableRow arg="interim-update" typ="alt { interim-update-disable: enum (disabled) { disabled:0 }
, interim-update-time: time
 }"></ArgTableRow>
<ArgTableRow arg="called-format" typ="enum (mac:ssid | mac | ssid)"></ArgTableRow>
</ArgTable>
