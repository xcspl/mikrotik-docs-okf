---
type: Reference
title: "Controller Bridge and Port Extender"
description: "The feature has been removed from RouterOS since v7.18."
timestamp: '2026-05-26'
status: active
tags: [routeros, mikrotik, networking]
resource: ~/Downloads/ROS-260526-1445-796.pdf
sources:
  - resource: https://manual.mikrotik.com/docs/introduction/
---

# Controller Bridge and Port Extender

Summary Limitations Quick setup Discovery and control protocols Packet flow Controller Bridge settings and monitoring Port Extender settings Configuration examples Basic CB and PE configuration Trunk and Access ports Cascading multiple Port Extenders and using bonding interface Configuration modification and removal

The feature has been removed from RouterOS since v7.18.

## <u>Summary</u>

Controller Bridge (CB) and Port Extender (PE) is an IEEE 802.1BR standard implementation in RouterOS for CRS3xx series switches. It allows virtually extending the CB ports with a PE device and manage these extended interfaces from a single controlling device. Such configuration provides a simplified network topology, flexibility, increased port density and ease of manageability. An example of Controller Bridge and Port Extender topology can be seen below.

|See supported features for each switch model below.||The Controller Bridge establishes communication with the Port Extender through a cascade port. Similarly, the Port Extender will communicate with the Controller Bridge only through an upstream port. On a PE device, control ports must be configured and only one port (closest to the CB) will act as an upstream port, other control ports can act as a backup for upstream port or even cascade port for switches connected in series (e.g. Port Extender 2 and 3 in the image above). Cascade and upstream ports are used to transmit and receive control and network traffic. Extended ports are interfaces that are controlled by the CB device and they are typically connected to the end hosts. Extended ports only transmit and receive network traffic.|
|---|---|---|
|Model|Controller Bridge|Port Extender|
|netPower 15FR (CRS318-1Fi-15Fr-2S)|-|+|
|netPower 16P (CRS318-16P-2S+)|-|+|
|CRS310-1G-5S-4S+ (netFiber 9/IN)|-|+|
|CRS326-24G-2S+ (RM/IN)|-|+|
|CRS328-24P-4S+|-|+|
|CRS328-4C-20S-4S+|-|+|
|CRS305-1G-4S+|-|+|
|CRS309-1G-8S+|+|+|
|CRS317-1G-16S+|+|+|

CRS312-4C+8XG + +

CRS326-24S+2Q+ + +

CRS354-48G-4S+2Q+ + +

CRS354-48P-4S+2Q+ + +

Limitations

Although controller allows to configure port extender interfaces, some bridging and switching features cannot be used or will not work properly. Below are the most common controller and extender limitations. The list might change along upcoming RouterOS releases.

Feature Support

Bonding for cascade and upstream ports +

Bridge VLAN filtering +

Bonding for extended ports-

Dot1x authenticator (server)-

Ingress and egress rate-

Mirroring-

Port ingress VLAN filtering-

Port isolation-

Storm control-

Switch rules (ACL)-

L3HW offloading-

MLAG-

## <u>Quick setup</u>

In this example, we will create a Controlling Bridge (e.g. a CRS317-1G-16S+ switch) that will connect to a single Port Extender (e.g. a CRS326-24G- 2S+ switch) through an SFP+1 interface.

First, configure a bridge with enabled VLAN filtering on a CB device:

|/interface bridge add name=bridge1 vlan-filtering=yes|
|---|
|/interface bridge port-controller set bridge=bridge1 cascade-ports=sfp-sfpplus1 switch=switch1|
|/interface bridge port-extender set control-ports=sfp-sfpplus1 switch=switch1|

On the same device, configure a port that is connected to the PE device and will act as cascade port:

Last, on a PE device, simply configure a control port, which will be selected as an upstream port:

Once PE and CB devices are connected, all interfaces that are on the same switch group (except for control ports) will be extended and can be further configured on a CB device. An automatic bridge port configuration will be applied on the CB device which adds all extended ports in a single bridge, this configuration can be modified afterward.

In order to exclude some port from being extended (e.g. for out-of-band management purposes), additionally, configure excluded-ports property.

Make sure not to include the cascade-ports and control-ports in any routing or bridging configurations. These ports are recommended only for a CB and PE usage.

## <u>Discovery and control protocols</u>

Before frame forwarding on extended ports is possible, Controlling Bridge and Port Extender must discover each other and exchange with essential information.

CB and PE enabled devices are using a neighbor discovery protocol LLDP with specific Port Extension TLV. This allows CB and PE devices to advertise their support on cascade and control ports.

CB and PE configuration can override the neighbor discovery settings, for example, if a cascade port is not included in a neighbor discovery interface list, the LLDP messages will be still sent.

Once LLDP messages are exchanged between CB and PE, a Control and Status Protocol (CSP) over an Edge Control Protocol (ECP) will initiate. The CSP is used between CB and PE to assert control and receive status information from the associated PE-it assigns unique IDs for extended ports, controls data-path settings (e.g. port VLAN membership) and sends port status information (e.g. interface stats, PoE-out monitoring). The ECP provides a reliable and sequenced frame delivery (encoded with EtherType 0x8940).

The current CB implementation does not support any failover techniques. Once the CB device becomes unavailable, the PE devices will lose all the control and data forwarding rules.
