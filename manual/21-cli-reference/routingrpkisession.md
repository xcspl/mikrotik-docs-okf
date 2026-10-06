---
type: Reference
title: "/routing/rpki/session"
description: "RouterOS directory reference for /routing/rpki/session"
timestamp: '2026-10-06'
status: active
tags: [routeros, mikrotik, manual, cli-reference]
resource: https://manual.mikrotik.com/docs/cli-reference/routing/rpki/session.md
sources:
  - resource: https://manual.mikrotik.com/docs/cli-reference/routing/rpki/session.md
---

-----------

## routing/rpki/session 
**Type:** Directory

<ArgTable c1="Read-only Argument" c2="Type" c3="Description">
<ArgTableRow arg="group" typ="enum"></ArgTableRow>
<ArgTableRow arg="address" typ="address (flags=46i)"></ArgTableRow>
<ArgTableRow arg="port" typ="num"></ArgTableRow>
<ArgTableRow arg="state" typ="enum (idle | connecting | prepare | loading | sync | error)"></ArgTableRow>
<ArgTableRow arg="version" typ="num"></ArgTableRow>
<ArgTableRow arg="session" typ="num"></ArgTableRow>
<ArgTableRow arg="serial" typ="num"></ArgTableRow>
<ArgTableRow arg="expires" typ="time"></ArgTableRow>
</ArgTable>
