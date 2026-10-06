---
type: Reference
title: "/routing/rip/neighbor"
description: "This submenu is used to define neighboring routers to exchange routing information with. Normally there is no need to add the neighbors, if multicasting is working properly within the network. If there are problems"
timestamp: '2026-10-06'
status: active
tags: [routeros, mikrotik, manual, cli-reference]
resource: https://manual.mikrotik.com/docs/cli-reference/routing/rip/neighbor.md
sources:
  - resource: https://manual.mikrotik.com/docs/cli-reference/routing/rip/neighbor.md
---

-----------

## routing/rip/neighbor 
**Type:** Directory

This submenu is used to define neighboring routers to exchange routing information with. Normally there is no need to add the neighbors, if multicasting is working properly within the network. If there are problems with exchanging routing information, neighbor routers can be added to the list. It will force the router to exchange the routing information with the neighbor using regular unicast packets.

<ArgTable c1="Flag" c2="Name" c3="Description">
<ArgTableRow arg="D" typ="dynamic">dynamic</ArgTableRow>
</ArgTable>

<ArgTable c1="Read-only Argument" c2="Type" c3="Description">
<ArgTableRow arg="instance" typ="enum"></ArgTableRow>
<ArgTableRow arg="address" typ="address (flags=46i)"></ArgTableRow>
<ArgTableRow arg="routes" typ="num"></ArgTableRow>
<ArgTableRow arg="packets-total" typ="num"></ArgTableRow>
<ArgTableRow arg="packets-bad" typ="num"></ArgTableRow>
<ArgTableRow arg="entries-bad" typ="num"></ArgTableRow>
<ArgTableRow arg="last-update" typ="time">Time from last update.</ArgTableRow>
</ArgTable>
