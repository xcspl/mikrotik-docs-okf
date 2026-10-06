---
type: Reference
title: "/openflow"
description: "This menu lists the configuration of OpenFlow clients"
timestamp: '2026-10-06'
status: active
tags: [routeros, mikrotik, manual, cli-reference]
resource: https://manual.mikrotik.com/docs/cli-reference/openflow.md
sources:
  - resource: https://manual.mikrotik.com/docs/cli-reference/openflow.md
---

-----------

## openflow 
**Package:** openflow
**Type:** Directory

This menu lists the configuration of OpenFlow clients.

<ArgTable c1="Flag" c2="Name" c3="Description">
<ArgTableRow arg="X" typ="disabled"></ArgTableRow>
</ArgTable>

<ArgTable c1="Argument" c2="Type" c3="Description">
<ArgTableRow arg="name" typ="string" mandatory="1">Reference name of the entry</ArgTableRow>
<ArgTableRow arg="datapath-id" typ="super { number: num [0 .. 65535]
, [mac-address] /macAddr
 }">Datapath ID consisting of two parts (integer number [0..65535] and MAC address) separated by a slash.</ArgTableRow>
<ArgTableRow arg="version" typ="enum (default | 1 | 1.3)">Version of the OpenFlow standard to be used.</ArgTableRow>
<ArgTableRow arg="passive-port" typ="num">The port on which the OpenFlow agent listens for connections from the controller.</ArgTableRow>
<ArgTableRow arg="controllers" typ="object { contr: super { controler-protocol: enum (tcp | tls)
, [controller-address] /ip6Addr
, [controller-port] /num [1 .. 65535]
 }
 }">Configuration of the connection to the controller. Supported protocols are **tcp** and **tls**. Example: `tcp/1.2.3.4/6654`.</ArgTableRow>
<ArgTableRow arg="certificate" typ="enum (none)" unset="1">[Certificate from certificate store](https://manual.mikrotik.com/authentication-authorization-accounting/certificates). Used together with the `verify-peer` parameter.</ArgTableRow>
<ArgTableRow arg="verify-peer" typ="enum (required | none | if-cert-present)" unset="1">Verify peer's identity against the router's [certificate store](https://manual.mikrotik.com/authentication-authorization-accounting/certificates).</ArgTableRow>
<ArgTableRow arg="isolate-controllers" typ="bool" unset="1">Whether to isolate the configured controllers from each other.</ArgTableRow>
</ArgTable>

<ArgTable c1="Read-only Argument" c2="Type" c3="Description">
<ArgTableRow arg="openflow-fast-path-packets" typ="num">Number of packets sent to fast path.</ArgTableRow>
<ArgTableRow arg="openflow-fast-path-bytes" typ="num">Number of bytes set to fast path.</ArgTableRow>
</ArgTable>
