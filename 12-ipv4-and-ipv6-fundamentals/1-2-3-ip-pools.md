---
type: Reference
title: "IP Pools"
description: "IP pools are used to define range of IP addresses that can be used by various RouterOS utilities, for example, DHCP server, Point-to-Point servers and more. Separate lists for IPv4 and IPv6 are available. Whenever possib."
timestamp: '2026-05-26'
status: active
tags: [routeros, mikrotik, networking]
resource: ~/Downloads/ROS-260526-1445-796.pdf
sources:
  - resource: https://manual.mikrotik.com/docs/introduction/
---

# IP Pools

Summary IPv4 Pool Example Used addresses IPv6 Pool Example Used addresses

## Summary

IP pools are used to define range of IP addresses that can be used by various RouterOS utilities, for example, DHCP server, Point-to-Point servers and more. Separate lists for IPv4 and IPv6 are available. Whenever possible, the same IP address is given out to each client (OWNER/INFO pair).

## IPv4 Pool

Sub-menu: /ip pool

Property Description

comment (string; Short description of the pool Default: )

name (string; Unique identifier of the pool Default: )

next-pool (string; When IP address acquisition is performed a pool that has no free addresses, and the next-pool property is set, then IP Default: ) address will be acquired from next-pool

ranges (IP; Default: ) IP address list of non-overlapping IP address ranges in the form of: from1-to1,from2-to2,...,fromN-toN. For example, 10.0.0.1-

10.0.0.27,10.0.0.32-10.0.0.47
Example

To define a pool named "my-pool" with the 10.0.0.1-10.0.0.126 address range excluding gateway's address 10.0.0.1 and server's address 10.0.0.100, and the other pool dhcp-pool, with the 10.0.0.200-10.0.0.250 address range:

[admin@MikroTik] ip pool> add name=my-pool ranges=10.0.0.2-10.0.0.99,10.0.0.101-10.0.0.126 [admin@MikroTik] ip pool> add name=dhcp-pool ranges=10.0.0.200-10.0.0.250 [admin@MikroTik] ip pool> print # NAME RANGES 0 ip-pool 10.0.0.2-10.0.0.99

10.0.0.101-10.0.0.126 1 dhcp-pool 10.0.0.200-10.0.0.250
### Used addresses

Sub-menu: /ip pool used

Here you can see all used IP addresses from IP pools.

Read-only properties

Property Description

|address (IP) info (string) owner (string) pool (string) IPv6 Pool|Sub-menu: /ipv6 pool|Name of the IP pool|IP address that is assigned to client from the pool For DHCP MAC address from leases menu and for PPP connections username of PPP type client Service which is using this IP address|
|---|---|---|---|
|Property|||Description|
|Read-only properties|name (string; Default:) prefix (IPv6/0..128; Default:) from-pool (string; Default:)|prefix-length (integer [1..128]; Default:)|Descriptive name of the pool. Ipv6 address prefix The option represents the prefix size that will be given out to the client. Name of another pool from which to acquire prefix dynamically.|
|Property||Description||
|Example|dynamic (yes | no) expire-time (time) [admin@test-host] /ipv6 pool> add name: test prefix: 2001::/60 prefix-length: 62 # NAME PREFIX PREFIX-LENGTH 0 test 2001::/60 62bits|The example will create a pool of "2001::/60" to give out /62 prefixes: [admin@test-host] /ipv6 pool> print|Whether the pool is dynamic. Expire time is set to dynamic pools added by DHCPv6 client.|
|Read-only properties|Used addresses Sub-menu: /ipv6 pool used|||
|Property||Description||
|info (string) owner (string) pool (string)|prefix (IPv6/0..128)|Name of the pool.|Shows DUID related information received from the client (value in hex). Can contain also a raw timestamp in hex. What reserved the prefix ("DHCP", etc.) IPv6 prefix that is assigned to the client from the pool.|
