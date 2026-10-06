---
type: Reference
title: "/routing/bgp/session/clear"
description: "Clear the session flags. For example, to be able to re-establish a session after the prefix limit is reached 'limit-exceeded' flag must be cleared. It can be done by specifying flag parameter, which is able to take"
timestamp: '2026-10-06'
status: active
tags: [routeros, mikrotik, manual, cli-reference]
resource: https://manual.mikrotik.com/docs/cli-reference/routing/bgp/session/clear.md
sources:
  - resource: https://manual.mikrotik.com/docs/cli-reference/routing/bgp/session/clear.md
---

-----------

## routing/bgp/session/clear 
**Conditions:** !smips
**Type:** Command

Clear the session flags. For example, to be able to re-establish a session after the prefix limit is reached "limit-exceeded" flag must be cleared. It can be done by specifying `flag` parameter, which is able to take the following values:

* input-last-notification  
* limit-exceeded  
* output-last-notification  
* refused-cap-opt  
* stopped

<ArgTable c1="Argument" c2="Type" c3="Description">
<ArgTableRow arg="flag" typ="enum (refused-cap-opt | stopped | limit-exceeded | input-last-notification | output-last-notification)">A flag to be cleared from BGP session.</ArgTableRow>
</ArgTable>
