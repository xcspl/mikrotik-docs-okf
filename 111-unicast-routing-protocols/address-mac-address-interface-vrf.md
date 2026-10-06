---
type: Reference
title: "ADDRESS MAC-ADDRESS INTERFACE VRF"
description: "MikroTik RouterOS implements RIP version 2 (RFC 2453). Version 1 (RFC 1058) is not supported."
timestamp: '2026-05-26'
status: active
tags: [routeros, mikrotik, networking]
resource: ~/Downloads/ROS-260526-1445-796.pdf
sources:
  - resource: https://manual.mikrotik.com/docs/introduction/
---

# ADDRESS MAC-ADDRESS INTERFACE VRF

0 DR fe80::de2c:6eff:fec5:a7ff DC:2C:6E:C5:A7:FF sfp-sfpplus1 main

Now we can add unnumbered connection config:

/routing bgp connection

add instance=myInstance local.address=sfp-sfpplus1 .role=ibgp name=unnumbered_2

[admin@CCR2004_2XS_111] /routing/bgp/connection> print

Flags: D-DYNAMIC, X-DISABLED, I-INACTIVE

0 name="unnumbered_2" instance=v6_test

local.address=sfp-sfpplus1 .default-address=fe80::de2c:6eff:fea4:b42f%sfp-sfpplus1 .role=ibgp

routing-table=main as=333

[admin@CCR2004_2XS_111] /routing/bgp/session> print

Flags: E-ESTABLISHED

0 E name="unnumbered_2-1" instance=v6_test

remote.address=fe80::de2c:6eff:fec5:a7ff%sfp-sfpplus1 .as=333 .id=203.0.113.2 .capabilities=mp,rr,enhe,gr,as4 .afi=ipv6

.messages=5181 .bytes=98439 .eor=""

local.role=ibgp .address=fe80::de2c:6eff:fea4:b42f%sfp-sfpplus1 .as=333 .id=203.0.113.1 .cluster-id=203.0.113

.1 .capabilities=mp,rr,enhe,gr,as4 .afi=ipv6 .messages=5181 .bytes=98439 .eor="" output.procid=20 input.procid=20 ibgp multihop=yes hold-time=3m keepalive-time=1m uptime=3d14h20m55s640ms last-started=2026-02-12 18:26:59 prefix- count=0

RIP

Summary

Summary

MikroTik RouterOS implements RIP version 2 (RFC 2453). Version 1 (RFC 1058) is not supported.

RIP enables routers in an autonomous system to exchange routing information. It always uses the best path (the path with the fewest number of hops (i.e. routers)) available.
