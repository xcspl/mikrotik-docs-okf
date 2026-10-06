---
type: Reference
title: "HWMPplus mesh"
description: "This example uses static WDS links that are dynamically added as mesh ports when they become active. Two different frequencies are used: one for AP interconnections, and one for client connections to APs, so the AP must ."
timestamp: '2026-05-26'
status: active
tags: [routeros, mikrotik, networking]
resource: ~/Downloads/ROS-260526-1445-796.pdf
sources:
  - resource: https://help.mikrotik.com/docs/spaces/ROS/pages/328059/RouterOS
---

# HWMPplus mesh

## Summary

/interface mesh

HWMP+ is a MikroTik specific layer-2 routing protocol for wireless mesh networks. It is based on Hybrid Wireless Mesh Protocol (HWMP) from IEEE

802.11s draft standard. It can be used instead of (Rapid) Spanning Tree protocols in mesh setups to ensure loop-free optimal routing. The HWMP+ protocol however is not compatible with HWMP from IEEE 802.11s draft standard. Note that the distribution system you use for your network need not be a Wireless Distribution System (WDS). HWMP+ mesh routing supports not only WDS interfaces but also Ethernet interfaces inside the mesh. So you can use a simple Ethernet-based distribution system, or you can combine both WDS and Ethernet links! HWMPplus is not supported on Wifi interfaces, but can be used on Wireless interfaces.
## Properties

Mesh

Property

admin-mac (MAC address; Default: 00:00:00:00:00:00)

arp (disabled | enabled | proxy-arp | reply-only; Default: enabled)

auto-mac (boolean; Default: no)

hwmp-default-hoplimit (inte ger: 1..255; Default: )

hwmp-prep-lifetime (time; Default: 5m)

hwmp-preq-destination-only (boolean; Default: yes)

hwmp-preq-reply-and- forward (boolean; Default: y es)

hwmp-preq-retries (integer; Default: )2

hwmp-preq-waiting-time (ti me; Default: 4s)

hwmp-rann-interval (time; Default: 10s)

hwmp-rann-lifetime (time; Default: 1s)

hwmp-rann-propagation- delay (number; Default: 0.5)

Description

Administratively assigned MAC address, used when the auto-mac setting is disabled

Address Resolution Protocol setting

If disabled, then the value from admin-mac will be used as the MAC address of the mesh interface; else address of some port will be used if ports are present

Maximum hop count for generated routing protocol packets; after an HWMP+ packet is forwarded "hoplimit" times, it is dropped

Lifetime for routes created from received PREP or PREQ messages

Whether the only destination can respond to HWMP+ PREQ message

Whether intermediate nodes should forward HWMP+ PREQ message after responding to it. Useful only when hwmp-preq- destination-only is disabled

How many times to retry a route discovery to a specific MAC address before the address is considered unreachable

How long to wait for a response to the first PREQ message. Note that for subsequent PREQs the waiting time is increased exponentially

How often to send out HWMP+ RANN messages

Lifetime for routes created from received RANN messages

How long to wait before propagating a RANN message. Value in seconds

mesh-portal (boolean; Whether this interface is a portal in the mesh network Default: no)

mtu (number; Default: 1500) Maximum transmission unit size

name (string; Default: ) Interface name

reoptimize-paths (boolean; Whether to send out periodic PREQ messages asking for known MAC addresses. Turning on this setting is useful if the Default: no) network topology is changing often. Note that if no reply is received to a re-optimization PREQ, the existing path is kept anyway (until it timeouts itself)

Port

Property Description

active-port-type (read-only: wireless | WDS | ethernet-mesh port type and state actually used | ethernet-bridge | ethernet-mixed; Default: )

hello-interval (time; Default: 10s) the maximum interval between sending out HWMP+ Hello messages. Used only for Ethernet type ports

interface (interface name; Default: ) interface name, which is to be included in a mesh

mesh (interface name; Default: ) mesh interface this port belongs to

path-cost (integer: 0..65535; Default: 10) path cost to the interface, used by routing protocol to determine the 'best' path

port-type (WDS | auto | ethernet | wireless; Default: ) port type to use

auto-port type is determined automatically based on the underlying interface's type WDS-a Wireless Distribution System interface. Remote MAC address is learned from wireless connection data ethernet-Remote MAC addresses are learned either from HWMP+ Hello messages or from source MAC addresses in received or forwarded traffic wireless-Remote MAC addresses are learned from wireless connection data

### FDB Status

Property Description

mac-address (MAC address) MAC address corresponding for this FDB entry

seq-number (integer) sequence number used in routing protocol to avoid loops

type (integer) sequence number used in routing protocol to avoid loops

interface (local | outsider | direct | mesh | type of this FDB entry neighbor | larval | unknown) local -- MAC address belongs to the local router itself outsider -- MAC address belongs to a device external to the mesh network direct -- MAC address belongs to a wireless client on an interface that is in the mesh network mesh -- MAC address belongs to a device reachable over the mesh network; it can be either internal or external to the mesh network neighbor -- MAC address belongs to a mesh router that is a direct neighbor to this router larval -- MAC address belongs to an unknown device that is reachable over the mesh network unknown -- MAC address belongs to an unknown device

mesh (interface name) the mesh interface this FDB entry belongs to

on-interface (interface name) mesh port used for traffic forwarding, kind of a next-hop value

lifetime (time) time remaining to live if this entry is not used for traffic forwarding

age (time) age of this FDB entry

metric (integer) a metric value used by routing protocol to determine the 'best' path

## Example

This example uses static WDS links that are dynamically added as mesh ports when they become active. Two different frequencies are used: one for AP interconnections, and one for client connections to APs, so the AP must have at least two wireless interfaces. Of course, the same frequency for all connections also could be used, but that might not work as well because of potential interference issues.

Repeat this configuration on all APs:

/interface mesh add disabled=no /interface mesh port add interface=wlan1 mesh=mesh1 /interface mesh port add interface=wlan2 mesh=mesh1

# interface used for AP interconnections /interface wireless set wlan1 disabled=no ssid=mesh frequency=2437 band=2ghz-b/g/n mode=ap-bridge \ wds-mode=static-mesh wds-default-bridge=mesh1

# interface used for client connections /interface wireless set wlan2 disabled=no ssid=mesh-clients frequency=5180 band=5ghz-a/n/ac mode=ap-bridge

# a static WDS interface for each AP you want to connect to /interface wireless wds add disabled=no master-interface=wlan1 name=<descriptive name of remote end> \ wds-address=<MAC address of remote end>

Here WDS interface is added manually because static WDS mode is used. If you are using wds-mode=dynamic-mesh, all WDS interfaces will be created automatically. The frequency and band parameters are specified here only to produce valid example configuration; mesh protocol operations are by no means limited to or optimized for, these particular values.

You may want to increase disconnect-timeout wireless interface option to make the protocol more stable. the

In real-world setups you also should take care of securing the wireless connections, using /interface wireless security-profile. For simplicity, that configuration is not shown here.

Results on router A (there is one client connected to wlan2):

[admin@A] > /interface mesh print Flags: X-disabled, R-running 0 R name="mesh1" mtu=1500 arp=enabled mac-address=00:0C:42:0C:B5:A4 auto-mac=yes admin-mac=00:00:00:00:00:00 mesh-portal=no hwmp-default-hoplimit=32 hwmp-preq-waiting-time=4s hwmp-preq-retries=2 hwmp-preq-destination-only=yes hwmp-preq-reply-and-forward=yes hwmp-prep-lifetime=5m hwmp-rann-interval=10s hwmp-rann-propagation-delay=1s hwmp-rann-lifetime=22s

[admin@A] > /interface mesh port print detail Flags: X-disabled, I-inactive, D-dynamic 0 interface=wlan1 mesh=mesh1 path-cost=10 hello-interval=10s port-type=auto port-type-used=wireless 1 interface=wlan2 mesh=mesh1 path-cost=10 hello-interval=10s port-type=auto port-type-used=wireless 2 D interface=router_B mesh=mesh1 path-cost=105 hello-interval=10s port-type=auto port-type-used=WDS 3 D interface=router_D mesh=mesh1 path-cost=76 hello-interval=10s port-type=auto port-type-used=WDS

The FDB (Forwarding Database) at the moment contains information only about local MAC addresses, non-mesh nodes reachable through a local interface, and direct mesh neighbors:

[admin@A] /interface mesh fdb print Flags: A-active, R-root MESH TYPE MAC-ADDRESS ON-INTERFACE LIFETIME AGE A mesh1 local 00:0C:42:00:00:AA 3m17s A mesh1 neighbor 00:0C:42:00:00:BB router_B 1m2s A mesh1 neighbor 00:0C:42:00:00:DD router_D 3m16s A mesh1 direct 00:0C:42:0C:7A:2B wlan2 2m56s A mesh1 local 00:0C:42:0C:B5:A4 2m56s

[admin@A] /interface mesh fdb print detail Flags: A-active, R-root A mac-address=00:0C:42:00:00:AA type=local age=3m21s mesh=mesh1 metric=0 seqnum=4294967196 A mac-address=00:0C:42:00:00:BB type=neighbor on-interface=router_B age=1m6s mesh=mesh1 metric=132 seqnum=4294967196 A mac-address=00:0C:42:00:00:DD type=neighbor on-interface=router_D age=3m20s mesh=mesh1 metric=79 seqnum=4294967196 A mac-address=00:0C:42:0C:7A:2B type=direct on-interface=wlan2 age=3m mesh=mesh1 metric=10 seqnum=0 A mac-address=00:0C:42:0C:B5:A4 type=local age=3m mesh=mesh1 metric=0 seqnum=0

Test if ping works:

[admin@A] > /ping 00:0C:42:00:00:CC 00:0C:42:00:00:CC 64 byte ping time=108 ms 00:0C:42:00:00:CC 64 byte ping time=51 ms 00:0C:42:00:00:CC 64 byte ping time=39 ms 00:0C:42:00:00:CC 64 byte ping time=43 ms 4 packets transmitted, 4 packets received, 0% packet loss round-trip min/avg/max = 39/60.2/108 ms

Router A had to discover a path to Router C first, hence the slightly larger time for the first ping. Now the FDB also contains an entry for 00:0C:42:00:00: CC, with type "mesh".

Also, test that ARP resolving works and so does IP level ping:

[admin@A] > /ping 10.4.0.3

10.4.0.3 64 byte ping: ttl=64 time=163 ms
10.4.0.3 64 byte ping: ttl=64 time=46 ms
10.4.0.3 64 byte ping: ttl=64 time=48 ms 3 packets transmitted, 3 packets received, 0% packet loss round-trip min/avg/max = 46/85.6/163 ms
Mesh traceroute

There is also a mesh traceroute command, that can help you to determine which paths are used for routing.

For example, for this network:

[admin@1] /interface mesh fdb print Flags: A-active, R-root MESH TYPE MAC-ADDRESS ON-INTERFACE LIFETIME AGE A mesh1 local 00:0C:42:00:00:01 7m1s A mesh1 mesh 00:0C:42:00:00:02 wds4 17s 4s A mesh1 mesh 00:0C:42:00:00:12 wds4 4m58s 1s A mesh1 mesh 00:0C:42:00:00:13 wds4 19s 2s A mesh1 neighbor 00:0C:42:00:00:16 wds4 7m1s A mesh1 mesh 00:0C:42:00:00:24 wds4 18s 3s

Traceroute to 00:0C:42:00:00:12 shows:

[admin@1] /interface mesh traceroute mesh1 00:0C:42:00:00:12 ADDRESS TIME STATUS 00:0C:42:00:00:16 1ms ttl-exceeded 00:0C:42:00:00:02 2ms ttl-exceeded 00:0C:42:00:00:24 4ms ttl-exceeded 00:0C:42:00:00:13 6ms ttl-exceeded 00:0C:42:00:00:12 6ms success

## Protocol description

### Reactive mode

Router A wants to discover a path to C

Router C sends a unicast response to A

In reactive mode, HWMP+ is very much like AODV (Ad-hoc On-demand Distance Vector). All paths are discovered on-demand, by flooding Path Request (PREQ) message in the network. The destination node or some router that has a path to the destination will reply with a Path Response (PREP). Note that if the destination address belongs to a client, the AP this client is connected to will serve as a proxy for him (i.e. reply to PREQs on his behalf).

This mode is best suited for mobile networks, and/or when most of the communication happens between intra-mesh nodes.

### Proactive mode

The root announces itself by flooding RANN

Internal nodes respond with PREGs

In proactive mode, there are some routers configured as portals. In general, being a portal means that the router has interfaces to some other network, i.e. it is an entry/exit point to the mesh network.

The portals will announce their presence by flooding the Root Announcement (RANN) message in the network. Internal nodes will reply with a Path Registration (PREG) message. The result of this process will be routing trees with roots in the portal.

Routes to portals will serve as a kind of default route. If an internal router does not know the path to a particular destination, it will forward all data to its closest portal. The portal will then discover the path on behalf of the router if needed. The data afterward will flow through the portal. This may lead to sub- optimal routing unless the data is addressed to the portal itself or some external network the portals have interfaces to.

A proactive mode is best suited when most of the traffic goes between internal mesh nodes and a few portal nodes.

### Topology change detection

Data flow path

After the link disappears, an error is propagated upstream

HWMP+ uses Path Error (PERR) message to notify that a link has disappeared. The message is propagated to all upstream nodes up to the data source. The source on PERR reception restarts the path discovery process.

FAQ

Q. How is this better than RSTP?
A. It gives you optimal routing. RSTP is only for loop prevention.
Q. How the route selection is done?
A. The route with the best metric is always selected after the discovery process. There is also a configuration option to periodically reoptimize already known routes. Route metric is calculated as the sum of individual link metrics. Link metric is calculated in the same way as for (R)STP protocols: For Ethernet links the metric is configured statically (same as for OSPF, for example). For WDS links the metric is updated dynamically depending on actual link bandwidth, which in turn is influenced by wireless signal strength, and the selected data transfer rate. Currently, the protocol does not take into account the amount of bandwidth being used on a link, but that might be also used in the future.
Q. How is this better than OSPF/RIP/layer-3 routing in general?
A. WDS networks usually are bridged, not routed. The ability to self-configure is important for mesh networks, and routing generally requires much more configuration than bridging. Of course, you can always run any L3 routing protocol over a bridged network, but for mesh networks that usually makes little sense.

Since optimized layer-2 multicast forwarding is not included in the mesh protocol, it is better to avoid forwarding any multicast traffic (including OSPF) over meshed networks. If you need OSPF, then you have to configure OSPF NBMA neighbors that use unicast mode instead.

Q. What about performance/CPU requirements?
A. The protocol itself, when properly configured, will take much fewer resources than OSPF (for example) would. Data forwarding performance on an individual router should be close to that of bridging.
Q. How does it work together with existing mesh setups that are using RSTP?
A. The internal structure of an RSTP network is transparent to the mesh protocol (because mesh hello packets are forwarded inside the RSTP network). The mesh will see the path between two entry points in the RSTP network as a single segment. On the other hand, a mesh network is not transparent to the RSTP, since RSTP hello packets are not be forwarded inside the mesh network. (This is the behavior since v3.26) Routing loops are possible if a mesh network is attached to an RSTP network in two or more points! Note that if you have a WDS link between two access points, then both ends must have the same configuration (either as ports in a mesh on both ends or as ports in a bridge interface on both ends). You can also put a bridge interface as a mesh port (to be able to use a bridge firewall, for example).
Q. Can I have multiple entry/exit points to the network?
A. If the entry/exit points are configured as portals (i.e. proactive mode is used), each router inside the mesh network will select its closest portal and forward all data to it. The portal will then discover a path on behalf of the router if needed.
Q. How to control or filter mesh traffic?
A. At the moment the only way is to use a bridge firewall. Create a bridge interface, put the WDS interfaces and/or Ethernets in that bridge, and put that bridge in a mesh interface. Then configure bridge firewall rules. To match MAC protocol used for mesh traffic encapsulation, use MAC protocol number 0x9AAA, and to match mesh routing traffic, use MAC protocol number 0x9AAB. Example: interface bridge settings set use-ip-firewall=yes interface bridge filter add chain=input action=log mac-protocol=0x9aaa interface bridge filter add chain=input action=log mac-protocol=0x9aab It is perfectly possible to create mixed mesh/bridge setups that will not work (e.g. Problematic example 1 with bridge instead of a switch). The recommended fail-safe way that will always work is to create a separate bridge interface per each of the physical interfaces; then add all these bridge interfaces as mesh ports.
## Advanced topics

We all know that it's easy to make problematic layer-2 bridging or routing setups and it can be hard to debug them. (Compared to layer-3 routing setups.) So here are a few bad configuration examples that could create problems for you. Avoid them!

Problematic example 1: Ethernet switch inside a mesh

Router A is outside the mesh, all the rest of the routers are inside. For routers B, C, D all interfaces are added as mesh ports.

Router A will not be able to communicate reliably with router C. The problem manifests itself when D is the designated router for Ethernet; if B takes this role, everything is OK. The main cause of the problem is MAC address learning on Ethernet switch.

Consider what happens when router A wants to send something to C. We suppose router A either knows or floods data to all interfaces. Either way, data arrives at the switch. The switch, not knowing anything about the destination's MAC address, forwards the data to both B and D.

What happens now:

1. B receives the packet on a mesh interface. Since the MAC address is not local for B and B knows that he is not the designated router for the Ethernet network, he simply ignores the packet.
2. D receives the packet on a mesh interface. Since the MAC address is not local for B and D is the designated router for the Ethernet network, he initiates the path discovery process to C.
After path discovery is completed, D has information that C is reachable over B. Now D encapsulates the packet and forwards it back to the Ethernet network. The encapsulated packet is forwarded by the switch, received and forwarded by B, and received by C. So far everything is good.

Now C is likely to respond to the packet. Since B already knows where A is, he will decapsulate and forward the reply packet. But now the switch will learn that the MAC address of C is reachable through B! That means, next time when something arrives from A addressed to C, the switch will forward data only t o B (and B, of course, will silently ignore the packet)!

In contrast, if B took up the role of a designated router, everything would be OK, because traffic would not have to go through the Ethernet switch twice.

Troubleshooting: either avoid such setup or disable MAC address learning on the switch. Note that on many switches that is not possible.

Also note that there will be no problem, if either:

router A supports and is configured to use HWMP+; or Ethernet switch is replaced with a router that supports HWMP+ and has Ethernet interfaces added as mesh ports.

### Problematic example 2: wireless modes

Consider this (invalid) setup example:

Routers A and B are inside the mesh, router C: outside. For routers A and B all interfaces are added as mesh ports.

It is not possible to bridge wlan1 and wlan2 on router B now. The reason for this is pretty obvious if you understand how WDS works. For WDS communications four address frames are used. This is because for wireless multihop forwarding you need to know both the addresses of the intermediate hops, as well as the original sender and final receiver. In contrast, non-WDS 802.11 communication includes only three MAC addresses in a frame. That's why it's not possible to do multi-hop forwarding in station mode.

Troubleshooting: depends on what you want to achieve:

1. If you want router C to act as a repeater either for wireless or Ethernet traffic, configure the WDS link between router B and router C, and run mesh routing protocol on all nodes.
2. In other cases configure wlan2 on router B in AP mode and WLAN on router C in station mode.

Nv2

## Overview

Overview Nv2 protocol implementation status Compatibility and coexistence with other wireless protocols How Nv2 compares with Nstreme and 802.11 Nv2 vs 802.11 Nv2 vs Nstreme Configuring Nv2 Migrating to Nv2 Nv2 AP Synchronization Configuration example QoS in Nv2 network Nv2-qos=default Nv2-qos=frame-priority Security in Nv2 network

Nv2 protocol is a proprietary wireless protocol developed by MikroTik for use with Atheros 802.11 wireless chips. Nv2 is based on TDMA (Time Division Multiple Access) media access technology instead of CSMA (Carrier Sense Multiple Access) media access technology used in regular 802.11 devices.

TDMA media access technology solves hidden node problem and improves media usage, thus improving throughput and latency, especially in PtMP networks.

Nv2 is supported for Atheros 802.11n chips and legacy 802.11a/b/g chips starting from AR5212, but not supported on older AR5211 and AR5210 chips. This means that both - 11n and legacy devices can participate in the same network and it is not required to upgrade hardware to implement Nv2 in network.

Media access in Nv2 network is controlled by Nv2 Access Point. Nv2 AP divides time into fixed size "periods" which are dynamically divided into downlink (data sent from AP to clients) and uplink (data sent from clients to AP) portions, based on the queue state on AP and clients. Uplink time is further divided between connected clients based on their requirements for bandwidth. At the beginning of each period, AP broadcasts a schedule that tells clients when they should transmit and the amount of time they can use.

In order to allow new clients to connect, Nv2 AP periodically assigns uplink time for "unspecified" client-this time interval is then used by a fresh client to initiate registration to AP. Then AP estimates propagation delay between AP and client and starts periodically scheduling uplink time for this client in order to complete registration and receive data from client.

Nv2 implements dynamic rate selection on a per-client basis and ARQ for data transmissions. This enables reliable communications across Nv2 links.

For QoS Nv2 implements variable number of priority queues with built-in default QoS scheduler that can be accompanied with fine-grained QoS policy based on firewall rules or priority information propagated across network using VLAN priority or MPLS EXP bits.

Nv2 protocol limit is 511 clients per interface.

## Nv2 protocol implementation status

Nv2 has the following features:

TDMA media access WDS support QoS support with variable number or priority queues data encryption RADIUS authentication features statistics fields Fixed Downlink mode support Uplink/Downlink ratio support Nv2 AP synchronization experimental support

## Compatibility and coexistence with other wireless protocols

Nv2 protocol is not compatible to or based on any other available wireless protocols or implementations, either TDMA based or any other kind. This implies that only Nv2 supporting and enabled devices can participate in Nv2 network.

Regular 802.11 devices will not recognize and will not be able to connect to Nv2 AP. RouterOS devices that have Nv2 support (that is-have RouterOS version 5.0rc1 or higher) will see Nv2 APs when issuing scan command, but will only connect to Nv2 AP if properly configured.

As Nv2 does not use CSMA technology it may disturb any other network in the same channel. In the same way other networks may disturb Nv2 network, because every other signal is considered noise.

The key points regarding compatibility and coexistence:

only RouterOS devices will be able to participate in Nv2 network only RouterOS devices will see Nv2 AP when scanning Nv2 network will disturb other networks in the same channel Nv2 network may be affected by any (Nv2 or not) other networks in the same channel Nv2 enabled device will not connect to any other TDMA based network

## How Nv2 compares with Nstreme and 802.11

### Nv2 vs 802.11

The key differences between Nv2 and 802.11:

Media access is scheduled by AP-this eliminates hidden node problem and allows to implement centralized media access policy-AP controls how much time is used by every client and can assign time to clients according to some policy instead of every device contending for media access. Reduced propagation delay overhead-There are no per-frame ACKs in Nv2 - this significantly improves throughput, especially on long-distance links where data frame and following ACK frame propagation delay significantly reduces the effectiveness of media usage. Reduced per frame overhead-Nv2 implements frame aggregation and fragmentation to maximize assigned media usage and reduce per-frame overhead (interframe spaces, preambles).

### Nv2 vs Nstreme

The key differences between Nv2 and Nstreme:

Reduced polling overhead-instead of polling each client, Nv2 AP broadcasts an uplink schedule that assigns time to multiple clients, this can be considered "group polling" - no time is wasted for polling each client individually, leaving more time for actual data transmission. This improves throughput, especially in PtMP configurations. Reduced propagation delay overhead-Nv2 must not poll each client individually, this allows to create uplink schedule based on estimated distance (propagation delay) to clients such that media usage is most effective. This improves throughput, especially in PtMP configurations. More control over latency-reduced overhead, adjustable period size and QoS features allows for more control over latency in the network.

## Configuring Nv2

wireless-protocol setting controls which wireless protocol selects and uses. Note that the meaning of this setting depends on the interface role (either it is AP or client) that depends on interface mode setting. Find possible values of wireless-protocol and their meaning in table below.

|value|AP|client|
|---|---|---|
|unspecified|establish nstreme or 802.11 network based on old nstreme setting|connect to nstreme or 802.11 network based on old nstreme setting|
|any|same as unspecified|scan for all matching networks, no matter what protocol, connect using protocol of chosen network|
|802.11|establish 802.11 network|connect to 802.11 networks only|
|nstreme|establish Nstreme network|connect to Nstreme networks only|
|Nv2|establish Nv2 network|connect to Nv2 networks only|

Nv2-establish Nv2 network scan for Nv2 networks, if suitable network found-connect, otherwise scan for Nstreme networks, if nstreme-suitable network found-connect, otherwise scan for 802.11 network and if suitable network found -

802.11 connect. Nv2-establish Nv2 network
scan for Nv2 networks, if suitable network found-connect, otherwise scan for Nstreme networks and nstreme if suitable network found-connect

Note that wireless-protocol values Nv2-nstreme-802.11 and Nv2-nstreme DO NOT specify some hybrid or special kind of protocol-these values are implemented to simplify client configuration when protocol of network that client must connect to can change. Using these values can help in migrating network to Nv2 protocol.

Most of Nv2 settings are significant only to Nv2 AP-Nv2 client automatically adapts necessary settings from AP. The following settings are relevant to Nv2 AP:

Nv2-queue-count-specifies how many priority queues are used in Nv2 network. For more details see QoS in Nv2 network Nv2-qos-controls frame to priority queue mapping policy. For more details see QoS in Nv2 network Nv2-cell-radius-specifies distance to farthest client in Nv2 network in km. This setting affects the size of contention time slot that AP allocates for clients to initiate connection and also size of time slots used for estimating distance to client. If this setting is too small, clients that are farther away may have trouble connecting and/or disconnect with "ranging timeout" error. Although during normal operation the effect of this setting should be negligible, in order to maintain maximum performance, it is advised to not increase this setting if not necessary, so AP is not reserving time that is actually never used, but instead allocates it for actual data transfer. tdma-period-size-specifies size in ms of time periods that Nv2 AP uses for media access scheduling. Smaller period can potentially decrease latency (because AP can assign time for client sooner), but will increase protocol overhead and therefore decrease throughput. On the other hand

- increasing period will increase throughput but also increase latency. It may be required to increase this value for especially long links to get acceptable throughput. This necessity can be caused by the fact that there is "propagation gap" between downlink (from AP to clients) and uplink (from clients to AP) data during which no data transfer is happening. This gap is necessary because client must receive last frame from AP-this happens after propagation delay after AP's transmission, and only then client can transmit-as a result frame from client arrives at AP after propagation delay after client's transmission (so the gap is propagation delay times two). The longer the distance, the bigger is necessary propagation gap in every period. If propagation gap takes significant portion of period, actual throughput may become unacceptable and period size should get increased at the expense of increased latency. Basically value of this setting must be carefully chosen to maximize throughput but also to keep latency at acceptable levels. Nv2-mode-specifies to use dynamic or fixed downlink/uplink ratio. Default value is "dynamic-downlink";
"sync-master" - works as nv2-mode=fixed-downlink (so uses nv2-downlink-ratio), but allows slaves to sync to this master; "sync-slave" - tries to sync to master (or already synced slave) and adapt period-size and downlink ratio settings from master.

Nv2-downlink-ratio-specifies the Nv2 downlink ratio. Uplink ratio is automatically calculated from the downlink-ratio value. When using dynamic- downlink mode the downlink-ratio is also used when link get fully saturated. Minimum value is 20 and maximum 80. Default value is 50.

The follwing settings are significant on both-Nv2 AP and Nv2 client:

Nv2-security-specifies Nv2 security mode, for more details see Security in Nv2 network Nv2-preshared-key-specifies preshared key to be used, for more details see Security in Nv2 network nv2-sync-secret-specifies secret key for use in the Nv2 synchronization. Secret should match on Master and Slave devices in order to establish the synced state.

## Migrating to Nv2

Using wireless-protocol setting aids in migration or evaluating Nv2 protocol in existing networks really simple and reduce downtime as much as possible. These are the recommended steps:

upgrade AP to version that supports Nv2, but do not enable Nv2 on AP yet. upgrade clients to version that supports Nv2 configure all clients with wireless-protocol=Nv2-nstreme-802.11. Clients will still connect to AP using protocol that was used previously, because AP is not changed over to Nv2 yet configure Nv2 related settings on AP if it is necessary to use data encryption and secure authentication, configure Nv2 security related settings on AP and clients (refer to Security in Nv2 network). set wireless-protocol=Nv2 on AP. This will make AP to change to Nv2 protocol. Clients should now connect using Nv2 protocol. in case of some trouble you can easily switch back to previous protocol by simply changing it back to whatever was used before on AP. fine tune Nv2 related settings to get acceptable latency and throughput implement QoS policy for maximum performance.

The basic troubleshooting guide:

clients have trouble connecting or disconnect with "ranging timeout" error-check that Nv2-cell-radius setting is set appropriately unexpectedly low throughput on long distance links although signal and rate is fine-try to increase tdma-period-size setting

## Nv2 AP Synchronization

This feature will let multiple MikroTik Nv2 APs on the same location to coexist in a better fashion by reducing the interference between each other. This feature will synchronize the transmit/receive time windows of APs in the same frequency, so that all synced MikroTik Nv2 APs transmits/receives at the same time. That allows to reuse the same wireless frequency on the location for multiple APs giving more flexibility in frequency planning.

To make Nv2 synced setup:

For Nv2 Synchronization a Master Nv2 AP should be chosen and "nv2-mode=sync-master" should be specified together with "nv2-sync-secret". For Nv2 Slave APs the same wireless frequency as Master AP should be used and "nv2-mode=sync-slave" should be specified with the same "nv2-sync-secret" as the in Master AP configuration. When Master AP is enabled Slave APs will try start searching for Master AP by matching it against specified "nv2-sync-secret". After Master AP is found the Slave AP will calculate the distance to the Master AP as it is possible that Master AP is located not on the same location. Then Slave AP starts operating as AP and it adapts the period size and downlink ratio from the synced Master AP. In addition after the Slave AP is operational other Slave APs can use this Slave AP to sync with. Slave AP periodically listens for the Master AP and checks if the "nv2-sync-secret" still matches and adapts the parameters again. If Master AP interface is disabled/enabled all the Slaves will be also disabled and will start the synchronization process from the beginning. If Master AP stops working Slave APs also will stop working as they do not have sync information.

### Configuration example

Master AP: /interface wireless set wlan1 mode=ap-bridge ssid=Sector1 frequency=5220 nv2-mode=sync-master nv2-preshared- key=clients1 nv2-sync-secret=Tower1

Slave AP: /interface wireless set wlan1 mode=ap-bridge ssid=Sector2 frequency=5220 nv2-mode=sync-slave nv2-preshared- key=clients2 nv2-sync-secret=Tower1

Monitor interface on the Slave AP: [admin@SlaveAP] /interface wireless> monitor wlan1 status: running-ap channel: 5220/20/an wireless-protocol: nv2 noise-floor: -110dBm registered-clients: 1 authenticated-clients: 1 nv2-sync-state: synced nv2-sync-master: 4C:5E:0C:57:84:38 nv2-sync-distance: 1 nv2-sync-period-size: 2 nv2-sync-downlink-ratio: 50

Debug logs on the Master AP: 09:22:08 wireless,debug wlan1: 4C:5E:0C:57:85:BE attempts to sync

Debug logs on the Slave AP: 09:22:08 wireless,debug wlan1: attempting to sync to 4C:5E:0C:57:84:38 09:22:09 wireless,debug wlan1: synced to 4C:5E:0C:57:84:38

## QoS in Nv2 network

QoS in Nv2 is implemented by means of variable number of priority queues. Queue is considered for transmission based on rule recommended by 802.1D- 2004 - only if all higher priority queues are empty. In practice this means that at first all frames from queue with higher priority will be sent, and only then next queue is considered. Therefore QoS policy must be designed with care so that higher priority queues do not make lower priority queues starve.

QoS policy in Nv2 network is controlled by AP, clients adapt policy from AP. On AP QoS policy is configured with Nv2-queue-count and Nv2-qos parameters. Nv2-queue-count parameter specifies number of priority queues used. Mapping of frames to queues is controlled by Nv2-qos parameter.

Nv2-qos=default

In this mode outgoing frame at first is inspected by built-in QoS policy algorithm that selects queue based on packet type and size. If built-in rules do not match, queue is selected based on frame priority field, as in Nv2-qos=frame-priority mode.

Nv2-qos=frame-priority

In this mode QoS queue is selected based on frame priority field. Note that frame priority field is not some field in headers and therefore it is valid only while packet is processed by given device. Frame priority field must be set either explicitly by firewall rules or implicitly from ingress priority by frame forwarding process, for example, from MPLS EXP bits. For more information on frame priority field see:

EXP bit and MPLS Queuing WMM and VLAN priority

Queue is selected based on frame priority according to 802.1D recommended user priority to traffic class mapping. Mapping depends on number of available queues (Nv2-queue-count parameter). For example, if number of queues is 4, mapping is as follows (pay attention how this mapping resembles mapping used by WMM):

priority 0,3 -> queue 0 priority 1,2 -> queue 1 priority 4,5 -> queue 2 priority 6,7 -> queue 3

If number of queues is 2 (default), mapping is as follows:

priority 0,1,2,3 -> queue 0 priority 4,5,6,7 -> queue 1

If number of queues is 8 (maximum possible), mapping is as follows:

priority 1 -> queue 0 priority 2 -> queue 1 priority 0 -> queue 2 priority 3 -> queue 3 priority 4 -> queue 4 priority 5 -> queue 5 priority 6 -> queue 6 priority 7 -> queue 7

For other mappings, discussion on rationale for these mappings and recommended practices please see 802.1D-2004.

## Security in Nv2 network

Nv2 security implementation has the following features:

hardware accelerated data encryption using AES-CCM with 128 bit keys; 4-way handshake for key management (similar to that of 802.11i); preshared key authentication method (similar to that of 802.11i); periodically updated group keys (used for broadcast and multicast data).

Being proprietary protocol Nv2 does not use security mechanisms of 802.11, therefore security configuration is different. Interface using Nv2 protocol ignores security-profile setting. Instead, security is configured by the following interface settings:

Nv2-security-this setting enables/disables use of security in Nv2 network. Note that when security is enabled on AP, it will not accept clients with disabled security. In the same way clients with enabled security will not connect to unsecure APs.

Nv2-preshared-key-preshared key to use for authentication. Data encryption keys are derived from preshared key during 4-way handshake. Preshared key must be the same in order for 2 devices to establish connection. If preshared key will differ, connection will time out because remote party will not be able to correctly interpret key exchange messages.
