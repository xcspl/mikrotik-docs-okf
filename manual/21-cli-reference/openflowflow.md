---
type: Reference
title: "/openflow/flow"
description: "This menu lists the installed flows responsible for packet forwarding between OpenFlow ports"
timestamp: '2026-10-06'
status: active
tags: [routeros, mikrotik, manual, cli-reference]
resource: https://manual.mikrotik.com/docs/cli-reference/openflow/flow.md
sources:
  - resource: https://manual.mikrotik.com/docs/cli-reference/openflow/flow.md
---

-----------

## openflow/flow 
**Package:** openflow
**Type:** Directory

This menu lists the installed flows responsible for packet forwarding between OpenFlow ports.

<ArgTable c1="Flag" c2="Name" c3="Description">
<ArgTableRow arg="I" typ="inactive"></ArgTableRow>
</ArgTable>

<ArgTable c1="Read-only Argument" c2="Type" c3="Description">
<ArgTableRow arg="switch" typ="enum">Controller name that installed the rule.</ArgTableRow>
<ArgTableRow arg="version" typ="num">OpenFlow protocol version of the switch that installed the flow.</ArgTableRow>
<ArgTableRow arg="match" typ="string">Match fields the flow entry matches against.</ArgTableRow>
<ArgTableRow arg="actions" typ="string">Actions applied to packets that match the flow entry.</ArgTableRow>
<ArgTableRow arg="info" typ="string">Additional flow entry information, such as priority, timeouts, and cookie.</ArgTableRow>
<ArgTableRow arg="table-id" typ="num">ID of the table where the rule is located.</ArgTableRow>
<ArgTableRow arg="bytes" typ="num">Number of bytes matched by the rule.</ArgTableRow>
<ArgTableRow arg="packets" typ="num">Number of packets matched by the rule.</ArgTableRow>
<ArgTableRow arg="duration" typ="time">Time since the flow entry was installed.</ArgTableRow>
</ArgTable>
