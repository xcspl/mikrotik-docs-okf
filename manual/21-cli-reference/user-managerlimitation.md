---
type: Reference
title: "/user-manager/limitation"
description: "RouterOS directory reference for /user-manager/limitation"
timestamp: '2026-10-06'
status: active
tags: [routeros, mikrotik, manual, cli-reference]
resource: https://manual.mikrotik.com/docs/cli-reference/user-manager/limitation.md
sources:
  - resource: https://manual.mikrotik.com/docs/cli-reference/user-manager/limitation.md
---

-----------

## user-manager/limitation 
**Package:** userman-5
**Type:** Directory

<ArgTable c1="Argument" c2="Type" c3="Description">
<ArgTableRow arg="name" typ="string" mandatory="1"></ArgTableRow>
<ArgTableRow arg="download-limit" typ="num"></ArgTableRow>
<ArgTableRow arg="upload-limit" typ="num"></ArgTableRow>
<ArgTableRow arg="transfer-limit" typ="num"></ArgTableRow>
<ArgTableRow arg="uptime-limit" typ="time"></ArgTableRow>
<ArgTableRow arg="reset-counters-start-time" typ="date"></ArgTableRow>
<ArgTableRow arg="reset-counters-interval" typ="alt { constant: enum (disabled | hourly | daily | weekly | monthly)
, reset-counters-interval: time
 }"></ArgTableRow>
<ArgTableRow arg="rate-limit-rx" typ="num"></ArgTableRow>
<ArgTableRow arg="rate-limit-tx" typ="num"></ArgTableRow>
<ArgTableRow arg="rate-limit-burst-rx" typ="num"></ArgTableRow>
<ArgTableRow arg="rate-limit-burst-tx" typ="num"></ArgTableRow>
<ArgTableRow arg="rate-limit-burst-threshold-rx" typ="num"></ArgTableRow>
<ArgTableRow arg="rate-limit-burst-threshold-tx" typ="num"></ArgTableRow>
<ArgTableRow arg="rate-limit-burst-time-rx" typ="time"></ArgTableRow>
<ArgTableRow arg="rate-limit-burst-time-tx" typ="time"></ArgTableRow>
<ArgTableRow arg="rate-limit-min-rx" typ="num"></ArgTableRow>
<ArgTableRow arg="rate-limit-min-tx" typ="num"></ArgTableRow>
<ArgTableRow arg="rate-limit-priority" typ="num"></ArgTableRow>
</ArgTable>
