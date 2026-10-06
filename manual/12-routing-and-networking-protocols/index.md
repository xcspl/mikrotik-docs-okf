# Routing and Networking Protocols

* [Routing and Networking Protocols](routing-and-networking-protocols.md) - This section provides guides for RouterOS routing and networking protocols, covering routing decisions, policy routing, VRF, route filtering, and major protocols like BGP, OSPF, RIP, EVPN, MPLS, along with migration
* [Routing Decision](routing-decision.md) - Routing decision in MikroTik RouterOS involves selecting paths for packet transmission using FIB and RIB tables, managing connected networks, default routes, and hardware offloading for efficient packet forwarding
* [Moving from ROSv6 to ROSv7](moving-from-rosv6-to-rosv7.md) - This page documents the transition from RouterOS v6 to v7, highlighting key changes such as increased routing table limits, new /routing/table and /routing/rule menus, improved route processing speed, and differences
* [Routing Protocol Multi-core Support](routing-protocol-multi-core-support.md) - RouterOS v7 enables multi-core routing by distributing tasks like FIB updates, BGP processing, and protocol handling across separate processes. Each sub-task uses private or shared memory, with BGP input/output
* [Policy Routing](policy-routing.md) - Policy routing in RouterOS allows steering traffic based on criteria to specific gateways, using custom routing tables and rules. It supports dynamic routing decisions with firewall mangle marking or basic routing
* [VRF](vrf.md) - RouterOS enables creating multiple Virtual Routing and Forwarding (VRF) instances for BGP-based MPLS VPNs, allowing separate routing tables and IP prefix isolation. VRF configurations are managed via the /ip/vrf

## Unicast

* [Unicast routing protocols](unicast-routing-protocols.md) - This section provides guides for configuring and understanding unicast routing protocols including BGP, OSPF, RIP, IS-IS, BFD, RPKI, and EVPN in MikroTik RouterOS
* [BFD](bfd.md) - Bidirectional Forwarding Detection (BFD) is a low-latency protocol for detecting faults in network paths, operating independently of routing protocols. It uses UDP encapsulation with configurable ports and supports

## Unicast / BGP

* [BGP](bgp.md) - This page introduces BGP (Border Gateway Protocol) configuration in MikroTik RouterOS, covering basic setup and routing concepts for establishing external network connectivity using BGP
* [Understanding BGP](understanding-bgp.md) - Overview of BGP protocol basics
* [Peering Sessions](peering-sessions.md) - Introduction on how to establish BGP sessions
* [Nexthop Selection](nexthop-selection.md) - BGP nexthop selection procedures on input and output
* [Route Leak Prevention](route-leak-prevention.md) - Prevent and detect route leaks using BGP roles defined in RFC 9234
* [FAQ](faq.md) - Frequently asked questions

## Unicast

* [EVPN](evpn.md) - This page introduces EVPN technology for Layer 2 and 3 VPN services, detailing BGP control planes, MPLS/VXLAN encapsulations, and EVPN route types (Type-1 to Type-5). It explains NVO terminology like NVE, VNI, and
* [IS-IS](is-is.md) - IS-IS is an Interior Gateway Protocol used for distributing IP routing information within a single Autonomous System, operating as a link-state protocol that exchanges topology data between neighbors. It supports

## Unicast / OSPF

* [OSPF](ospf.md) - OSPF (Open Shortest Path First) is a routing protocol used in MikroTik RouterOS to dynamically exchange route information and determine the best paths for data transmission within a network
* [Understanding OSPF](understanding-ospf.md) - Overview of OSPF protocol basics
* [Neighbor Relationship](neighbor-relationship.md) - Introduction on how neighbor relationships and adjacencies are formed
* [Routing Table Calculation](routing-table-calculation.md) - Basic understanding of shortest path calculation
* [Areas and Virtual Links](areas-and-virtual-links.md) - Understand the concept of OSPF areas and virtual links
* [FAQ](faq-2.md) - Frequently asked questions

## Unicast

* [RIP](rip.md) - MikroTik RouterOS supports RIP version 2 for exchanging routing information within autonomous systems, selecting optimal paths based on hop count. Configuration is available under /routing/rip
* [RPKI](rpki.md) - RouterOS supports RPKI for BGP prefix validation using the Resource Public Key Infrastructure, enabling secure route origin verification via RTR protocol. Configuration includes setting up RTR servers and applying

## MPLS

* [MPLS](mpls.md) - MPLS is a routing technology that uses labels for faster packet forwarding instead of IP header analysis, with RouterOS supporting MPLS switching, LDP/RSVP-TE protocols, VPLS, and MP-BGP VPNs while excluding certain
* [EXP bit and MPLS Queuing](exp-bit-and-mpls-queuing.md) - This page explains the EXP bit in MPLS packets and how RouterOS handles it for QoS, including priority marking, queuing strategies, and MPLS mangle rules. It details how EXP bits are treated during packet switching,
* [LDP](ldp.md) - This page introduces MikroTik RouterOS's Label Distribution Protocol (LDP) for establishing IPv4/IPv6 Label Switched Paths (LSPs), detailing prerequisites like loopback IP addresses and IP connectivity, along with an
* [Traffic Eng](traffic-eng.md) - This page documents MikroTik RouterOS Traffic Engineering (TE) tunnel functionality, covering monitoring commands like monitor to track TE tunnel status and paths, along with reoptimization techniques using

## MPLS / VPLS

* [VPLS](vpls.md) - The VPLS page introduces MikroTik RouterOS's Virtual Private LAN Service (VPLS) interface, detailing its use as a transparent ethernet tunnel with LDP or MP-BGP protocols. It covers VPLS features like pseudowire
* [Control Word](control-word.md) - VPLS uses Control Words (CW) for packet fragmentation and reassembly in RouterOS, adding 4-byte overhead to handle L2MTU limitations. CW fields include flags, fragmentation indicators, length, and sequence numbers

## Multicast

* [Multicast Routing Protocols](multicast-routing-protocols.md) - This section provides configuration guidance for RouterOS multicast routing protocols including IGMP Proxy, PIM-SM, and group management features to manage multicast traffic flows
* [Group Management Protocol](group-management-protocol.md) - Group Management Protocol enables interfaces to receive multicast streams without dedicated clients, supporting IGMP and MLD protocols. It allows testing multicast routing by sending membership reports and responding
* [IGMP Proxy](igmp-proxy.md) - The IGMP Proxy feature in RouterOS enables multicast routing by forwarding IGMP frames, offering a simpler alternative to PIM-SM for certain topologies. It supports basic multicast forwarding with minimal resource
* [PIM-SM](pim-sm.md) - This page introduces IP Multicast and Protocol Independent Multicast - Sparse Mode (PIM-SM) in MikroTik RouterOS, explaining how it enables efficient data sharing across networks. It covers basic PIM-SM configuration
* [Route Distinguisher and Route Target](route-distinguisher-and-route-target.md) - Route Distinguisher (RD) adds unique prefixes to customer addresses for VRF differentiation, while Route Targets control BGP routing information exchange between instances
* [Route Selection and Filtering](route-selection-and-filtering.md) - Route filtering in MikroTik RouterOS uses script-like syntax to match prefixes and modify routing distances based on conditions, with properties categorized as readable or readable/writable for matchers and actions
