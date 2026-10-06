---
type: Reference
title: "Interface Lists"
description: "This menu contains information about all interface lists available on the router. There are four predefined lists-all (contains all interfaces), none (contain s no interfaces), dynamic (contains dynamic interfaces), and ."
timestamp: '2026-05-26'
status: active
tags: [routeros, mikrotik, networking]
resource: ~/Downloads/ROS-260526-1445-796.pdf
sources:
  - resource: https://manual.mikrotik.com/docs/introduction/
---

# Interface Lists

Summary Lists Members

## Summary

Allows defining a set of interfaces for easier interface management in the different interface-based configuration sections such as Neighbor Discovery, Firewall, Bridge, and Internet Detect.

## Lists

Sub-menu: /interface list

This menu contains information about all interface lists available on the router. There are four predefined lists-all (contains all interfaces), none (contain s no interfaces), dynamic (contains dynamic interfaces), and static (contains static interfaces). It is also possible to create additional interface lists.

Dynamic interfaces are interfaces that have a "dynamic" flag. Any interface that doesn't have a dynamic flag will be part of the static interface list.

Property Description

name (string) Name of the interface list

include (string) Defines interface list which members are included in the list. It is possible to add multiple lists separated by commas

exclude (string) Defines interface list which members are excluded from the list. It is possible to add multiple lists separated by commas

Members are added to the interface list in the following order:

1. include members are added to the interface list
2. exclude members are removed from the list
3. Statically configured members are added to the list
## Members

Sub-menu: /interface list member

This sub-menu contains information about statically configured interface members to each interface list. Note that dynamically added interfaces by include and exclude statements are not represented in this sub-menu.

Property Description

interface ( Name of the interface string)

list (string) Name of the interface list

Care must be taken when working with bridges and lists. Adding a bridge as a member is not the same as adding all its ports! And adding all slave ports as members is not the same as adding the bridge itself. This can particularly impact functionality of neighbor discovery.
