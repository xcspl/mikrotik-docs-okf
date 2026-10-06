---
type: Reference
title: "/tool/traffic-generator"
description: "RouterOS settings reference for /tool/traffic-generator"
timestamp: '2026-10-06'
status: active
tags: [routeros, mikrotik, manual, cli-reference]
resource: https://manual.mikrotik.com/docs/cli-reference/tool/traffic-generator.md
sources:
  - resource: https://manual.mikrotik.com/docs/cli-reference/tool/traffic-generator.md
---

-----------

## tool/traffic-generator 
**Type:** Settings Directory

<ArgTable c1="Argument" c2="Type" c3="Description">
<ArgTableRow arg="test-id" typ="num"></ArgTableRow>
<ArgTableRow arg="measure-out-of-order" typ="bool"></ArgTableRow>
<ArgTableRow arg="latency-distribution-max" typ="time"></ArgTableRow>
<ArgTableRow arg="stats-samples-to-keep" typ="num"></ArgTableRow>
</ArgTable>

<ArgTable c1="Read-only Argument" c2="Type" c3="Description">
<ArgTableRow arg="running" typ="bool"></ArgTableRow>
<ArgTableRow arg="latency-distribution-samples" typ="num"></ArgTableRow>
<ArgTableRow arg="latency-distribution-measure-interval" typ="string"></ArgTableRow>
</ArgTable>
