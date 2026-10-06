---
type: Reference
title: "/cmr/layout/link"
description: "Configuration for a specific link in a topology"
timestamp: '2026-10-06'
status: active
tags: [routeros, mikrotik, manual, cli-reference]
resource: https://manual.mikrotik.com/docs/cli-reference/cmr/layout/link.md
sources:
  - resource: https://manual.mikrotik.com/docs/cli-reference/cmr/layout/link.md
---

-----------

## cmr/layout/link 
**Package:** cmr
**Type:** Directory

Configuration for a specific link in a topology.

<ArgTable c1="Argument" c2="Type" c3="Description">
<ArgTableRow arg="layout" typ="enum" mandatory="1">Name of the layout where the link will be displayed.</ArgTableRow>
<ArgTableRow arg="node1" typ="enum" mandatory="1">Name of the first node in a link.</ArgTableRow>
<ArgTableRow arg="node2" typ="enum" mandatory="1">Name of the second node in a link.</ArgTableRow>
</ArgTable>

<ArgTable c1="Read-only Argument" c2="Type" c3="Description">
<ArgTableRow arg="links" typ="multi { array-id, array-id, link: super { port1: object
, [port2] --object
 }
 }">Detailed information about the link state, such as PoE status, interface names, and traffic information. Example: `ether1(,tx=85.9KiB,rx=10.8KiB)--ether23(poe=powered-on,tx=10.9KiB,rx=86.8KiB)`</ArgTableRow>
</ArgTable>
