---
type: Reference
title: "Address-lists"
description: "Firewall address lists allow a user to create lists of IP addresses grouped together under a common name. Firewall filter, mangle, and NAT facilities can then use those address lists to match packets against them."
timestamp: '2026-05-26'
status: active
tags: [routeros, mikrotik, networking]
resource: ~/Downloads/ROS-260526-1445-796.pdf
sources:
  - resource: https://help.mikrotik.com/docs/spaces/ROS/pages/328059/RouterOS
---

# Address-lists

Summary Properties

## Summary

/ip firewall address-list

Firewall address lists allow a user to create lists of IP addresses grouped together under a common name. Firewall filter, mangle, and NAT facilities can then use those address lists to match packets against them.

The address list records can also be updated dynamically via the action=add-src-to-address-list or action=add-dst-to-address-list item s found in NAT, Mangle, and Filter facilities.

Firewall rules with action add-src-to-address-list or add-dst-to-address-list work in passthrough mode, which means that the matched packets will be passed to the next firewall rules.

## Properties

|Property||Description|
|---|---|---|
|address (DNS Name | IP||A single IP address or range of IPs to add to the address list or DNS name. You can input for example, '192.168.0.0-|
|address/netmask | IP-IP;||192.168.1.255' and it will auto modify the typed entry to 192.168.0.0/23 on saving. IP-IP ranges are supported only for|
|Default: )||IPv4 addresses.|
|dynamic (yes, no)||Allows creating data entry with dynamic form.|
|list (string; Default: )||Name for the address list of the added IP address.|
|timeout (time; Default: )||Time after address will be removed from the address list. If the timeout is not specified, the address will be stored in the address list permanently.|
|creation-time (time; Default: )||The time when the entry was created.|

If the timeout parameter is not specified, then the address will be saved to the list permanently on the disk. If a timeout is specified, the address will be stored on the RAM and will be removed after a system's reboot.
