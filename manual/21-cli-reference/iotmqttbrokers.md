---
type: Reference
title: "/iot/mqtt/brokers"
description: "RouterOS directory reference for /iot/mqtt/brokers"
timestamp: '2026-10-06'
status: active
tags: [routeros, mikrotik, manual, cli-reference]
resource: https://manual.mikrotik.com/docs/cli-reference/iot/mqtt/brokers.md
sources:
  - resource: https://manual.mikrotik.com/docs/cli-reference/iot/mqtt/brokers.md
---

-----------

## iot/mqtt/brokers 
**Package:** iot
**Type:** Directory

<ArgTable c1="Flag" c2="Name" c3="Description">
<ArgTableRow arg="W" typ="Will message enabled"></ArgTableRow>
</ArgTable>

<ArgTable c1="Argument" c2="Type" c3="Description">
<ArgTableRow arg="name" typ="string" mandatory="1"></ArgTableRow>
<ArgTableRow arg="address" typ="string" mandatory="1"></ArgTableRow>
<ArgTableRow arg="port" typ="num"></ArgTableRow>
<ArgTableRow arg="ssl" typ="bool"></ArgTableRow>
<ArgTableRow arg="client-id" typ="string"></ArgTableRow>
<ArgTableRow arg="username" typ="string"></ArgTableRow>
<ArgTableRow arg="password" typ="string"></ArgTableRow>
<ArgTableRow arg="will-topic" typ="string"></ArgTableRow>
<ArgTableRow arg="will-message" typ="string"></ArgTableRow>
<ArgTableRow arg="will-qos" typ="num"></ArgTableRow>
<ArgTableRow arg="will-retain" typ="bool"></ArgTableRow>
<ArgTableRow arg="certificate" typ="enum (none)"></ArgTableRow>
<ArgTableRow arg="auto-connect" typ="bool"></ArgTableRow>
<ArgTableRow arg="keep-alive" typ="num"></ArgTableRow>
<ArgTableRow arg="parallel-scripts-limit" typ="num"></ArgTableRow>
</ArgTable>

<ArgTable c1="Read-only Argument" c2="Type" c3="Description">
<ArgTableRow arg="connected" typ="bool"></ArgTableRow>
</ArgTable>
