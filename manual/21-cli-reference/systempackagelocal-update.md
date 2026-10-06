---
type: Reference
title: "/system/package/local-update"
description: "Instead of connecting directly to MikroTik servers, you can upload package files to one of your local RouterOS devices and use it as a local package server"
timestamp: '2026-10-06'
status: active
tags: [routeros, mikrotik, manual, cli-reference]
resource: https://manual.mikrotik.com/docs/cli-reference/system/package/local-update.md
sources:
  - resource: https://manual.mikrotik.com/docs/cli-reference/system/package/local-update.md
---

-----------

## system/package/local-update 
**Type:** Directory

Instead of connecting directly to MikroTik servers, you can upload package files to one of your local RouterOS devices and use it as a local package server.

<ArgTable c1="Argument" c2="Type" c3="Description">
<ArgTableRow arg="download" typ="bool">Whether to download available packages from the local package server.</ArgTableRow>
</ArgTable>

<ArgTable c1="Read-only Argument" c2="Type" c3="Description">
<ArgTableRow arg="source" typ="alt { ipv6: ip6Addr
, ip: ipAddr
 }">IP address of the local package server.</ArgTableRow>
<ArgTableRow arg="name" typ="string">Name of the package.</ArgTableRow>
<ArgTableRow arg="version" typ="string">Version of the package.</ArgTableRow>
<ArgTableRow arg="status" typ="enum (installed | downloaded | downloading | scheduled | available) { installed:0, downloaded:1, downloading:2, scheduled:3, available:4 }">Current status of the package.</ArgTableRow>
<ArgTableRow arg="completed" typ="num">Download completion percentage.</ArgTableRow>
</ArgTable>
