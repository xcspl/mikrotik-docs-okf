---
type: Reference
title: "/routing/igmp-proxy"
description: "RouterOS settings reference for /routing/igmp-proxy"
timestamp: '2026-10-06'
status: active
tags: [routeros, mikrotik, manual, cli-reference]
resource: https://manual.mikrotik.com/docs/cli-reference/routing/igmp-proxy.md
sources:
  - resource: https://manual.mikrotik.com/docs/cli-reference/routing/igmp-proxy.md
---

-----------

## routing/igmp-proxy 
**Type:** Settings Directory

<ArgTable c1="Argument" c2="Type" c3="Description">
<ArgTableRow arg="robustness" typ="num">The robustness value of the IGMP proxy, used as the retransmission count for queries and the tolerance for lost packets. Interfaces without their own robustness setting inherit this value.</ArgTableRow>
<ArgTableRow arg="query-interval" typ="time">How often to send out IGMP Query messages over downstream interfaces.</ArgTableRow>
<ArgTableRow arg="query-response-interval" typ="time">How long to wait for responses to an IGMP Query message.</ArgTableRow>
<ArgTableRow arg="last-member-query-interval" typ="time">The timeout for group-specific queries sent to verify that no group members remain after a Leave message.</ArgTableRow>
</ArgTable>
