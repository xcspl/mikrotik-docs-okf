---
type: Reference
title: "Traffic Eng"
description: "Do not use interface if resource-class matches any of specified bits."
timestamp: '2026-05-26'
status: active
tags: [routeros, mikrotik, networking]
resource: ~/Downloads/ROS-260526-1445-796.pdf
sources:
  - resource: https://manual.mikrotik.com/docs/introduction/
---

# Traffic Eng

Properties

Sub-menu: /interface traffic-eng

Property

affinity-exclude (integer; Default: not set)

affinity-include-all (integer; Default: no t set)

affinity-include-any (integer; Default: n ot set)

auto-bandwidth-avg-interval (time; Default: 5m)

auto-bandwidth-range (Disabled | Min [bps][-Max[bps]]; Default: 0bps)

auto-bandwidth-reserve (integer[%]; Default: 0%)

auto-bandwidth-update-interval (time; Default: 1h)

bandwidth (integer[bps]; Default: 0bps)

bandwidth-limit (disabled | integer[%]; Default: disabled)

comment (string; Default: )

disable-running-check (yes | no; Default: no)

disabled (yes | no; Default: yes)

from-address (auto | IP; Default: auto)

holding-priority (integer [0..7]; Default: not set)

mtu (integer; Default: 1500)

name (string; Default: )

primary-path (string; Default: )

primary-retry-interval (time; Default: 1m )

record-route (yes | no; Default: not set)

reoptimize-interval (time; Default: not set)

secondary-paths (string[,string]; Default: )

Description

Do not use interface if resource-class matches any of specified bits.

Use interface only if resource-class matches all of specified bits.

Use interface if resource-class matches any of specified bits.

Interval in which actual amount of data is measured, from which average bandwidth is calculated.

Auto bandwidth adjustment range. Read more >>

Specifies percentage of additional bandwidth to reserve. Read more >>

Interval during which tunnel keeps track of highest average rate.

How much bandwidth to reserve for TE tunnel. Value is in bits per second. Read more >>

Defines actual bandwidth limitation of TE tunnel. Limit is configured in percent of specified tunnel bandwidth. Read more >>

Short description of the item

Specifies whether to detect if interface is running or not. If set to no interface will always have running flag.

Defines whether item is ignored or used.

Ingress address of the tunnel. If set to auto least IP address is picked.

Is used to decide whether this session can be preempted by another session. 0 sets the highest priority.

Layer3 Maximum Transmission Unit

Name of the interface

Primary label switching paths defined in /mpls traffic-eng tunnel-path menu.

Interval after which tunnel will try to use primary path.

If enabled, the sender node will receive information about the actual route that the LSP tunnel traverses. Record Route is analogous to a path vector, and hence can be used for loop detection.

Interval after which tunnel will re-optimize current path. If current path is not the best path then after optimization best path will be used. Read more >>

List of label switching paths used by TE tunnel if primary path fails. Paths are defined in /mpls traffic- eng tunnel-path menu.

|setup-priority (integer[0..7]; Default: n ot set) to-address (IP; Default: 0.0.0.0) Monitoring To verify TE tunnel's status|Remote end of TE tunnel. monitor command can be used.|Parameter is used to decide whether this session can preempt another session. 0 sets the highest priority.|
|---|---|---|
|/interface traffic-eng monitor 0 tunnel-id: 12 primary-path-state: on-hold secondary-path: static active-path: static active-lspid: 3 active-label: 66 reserved-bandwidth: 5.0Mbps|secondary-path-state: established explicit-route: "S:192.168.55.10/32,L:192.168.55.13/32,L:192.168.55.17/32" recorded-route: "192.168.55.13[66],192.168.55.17[59],192.168.55.18[3]"||
|Reoptimization other factors. alues if record-route parameter is enabled. /interface traffic-eng monitor 0 tunnel-id: 12 primary-path-state: established primary-path: dyn active-path: dyn active-lspid: 1 active-label: 67 reserved-bandwidth: 5.0Mbps manually reoptimize the tunnel path.|Path can be re-optimized manually by entering the command /interface traffic-eng reoptimize [id] (where [id] is an item number or interface name). It allows network administrators to reoptimize the LSPs that have been established based on changes in bandwidth, traffic, management policy, or Let's say TE tunnel chose another path after a link failure on best path. You can verify optimization by looking at secondary-path-state: not-necessary explicit-route: "S:192.168.55.10/32,S:192.168.55.13/32,S:192.168.55.14/32, S:192.168.55.17/32,S:192.168.55.18/32" recorded-route: "192.168.55.13[67],192.168.55.17[60],192.168.55.18[3]" Whenever the link comes back, TE tunnel will use the same path even it is not the best path (unless reoptimize-interval is configured). To fix it we can /interface traffic-eng reoptimize 0|explicit-route or recorded-route|

v

/interface traffic-eng monitor 0 tunnel-id: 12 primary-path-state: established primary-path: dyn secondary-path-state: not-necessary active-path: dyn active-lspid: 2 active-label: 81 explicit-route: "S:192.168.55.5/32,S:192.168.55.2/32,S:192.168.55.1/32" recorded-route: "192.168.55.2[81],192.168.55.1[3]" reserved-bandwidth: 5.0Mbps

Notice how explicit-route and recorded-route changed to a shorter path.
