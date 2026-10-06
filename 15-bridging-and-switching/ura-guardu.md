---
type: Reference
title: "<u>RA Guard</u>"
description: "The RA guard feature is intended for discarding IPv6 packets containing router advertisement (RA) messages arriving on bridge ports specified by the user as untrusted ones, thereby allowing one to prevent potential rogue."
timestamp: '2026-05-26'
status: active
tags: [routeros, mikrotik, networking]
resource: ~/Downloads/ROS-260526-1445-796.pdf
sources:
  - resource: https://manual.mikrotik.com/docs/introduction/
---

# <u>RA Guard</u>

The RA guard feature is intended for discarding IPv6 packets containing router advertisement (RA) messages arriving on bridge ports specified by the user as untrusted ones, thereby allowing one to prevent potential rogue RA message-based attacks or accidental network misconfiguration. When enabled, it is possible to set each bridge ports either as trusted, or untrusted (by default all the bridge ports are set as RA untrusted).

Here is the network scheme and core principle behind IPv6 RA Guard (Router Advertisement Guard).

#Layer 2 Access Switch-enabling RA guard on the main bridge /interface bridge add name=bridge /interface bridge set [find where name="bridge"] ra-guard=yes /interface bridge port add bridge=bridge interface=etherUplink Trusted RA=yes add bridge=bridge interface=etherX add bridge=bridge interface=etherY add bridge=bridge interface=etherZ

The Problem: Why is this needed?

In IPv6, devices use ICMPv6 to auto-configure themselves.

Router Advertisements (Type 134): Routers broadcast these messages to tell hosts: "I am the gateway, and here is your network prefix."

The Threat: If a user accidentally connects a consumer router (like a home Wi-Fi router) or a malicious actor launches a tool (like Rogue RA) on an access port, that device will start broadcasting RAs.

The Result: Other hosts on the network will auto-configure their IPv6 addresses based on the rogue device and set the rogue device as their default gateway. This causes a Man-in-the-Middle attack or a complete denial of service.

Here is the network scheme and core principle behind IPv6 RA Guard (Router Advertisement Guard).

The Core Principle: "Trust vs. Untrust"

The fundamental principle of IPv6 RA Guard is logically identical to DHCP Snooping in IPv4. It creates a security boundary within the Layer 2 switch infrastructure by categorizing switch ports into two roles:

Trusted Ports: Ports connected to legitimate, authorized IPv6 routers. These ports are allowed to send Router Advertisement (RA) packets. Untrusted Ports: Ports connected to end-user hosts. These ports are blocked from sending RA packets.

Packet parsing process

For ports not configured as RA Trusted, the RA Guard parser traverses the extension header chain until it encounters a non-extension header. The parsing process and subsequent actions are governed by the following rules:

Transport Layer Termination: If the parser encounters a valid transport layer header—such as TCP, UDP, ESP, RSVP, or an encapsulated IPv4/IPv6 header—parsing terminates and the packet is forwarded (subject to standard bridge checks).

Drop Conditions-The packet is discarded if:

1. It fails to contain a transport layer header.
2. The final extension header in the chain does not specify NO_NEXT_HEADER (59) in its "Next Header" field.
3. If the ICMP message type is found to be 134, the packet is dropped.
Fragmentation Handling: These parsing rules apply exclusively to the first fragment of fragmented IPv6 packets. Subsequent fragments are forwarded regardless of their content, as they do not contain the protocol headers necessary for RA identification.

## <u>Bridge Firewall</u>

The bridge firewall implements packet filtering and thereby provides security functions that are used to manage data flow to, from, and through the bridge.

Packet flow diagram shows how packets are processed through the router. It is possible to force bridge traffic to go through /ip firewall filter r ules (see the bridge settings).

There are two bridge firewall tables:

filter-bridge firewall with three predefined chains: input-filters packets, where the destination is the bridge (including those packets that will be routed, as they are destined to the bridge MAC address anyway) output-filters packets, which come from the bridge (including those packets that has been routed normally) forward-filters packets, which are to be bridged (note: this chain is not applied to the packets that should be routed through the router, just to those that are traversing between the ports of the same bridge) nat-bridge network address translation provides ways for changing source/destination MAC addresses of the packets traversing a bridge. Has two built-in chains: srcnat-used for "hiding" a host or a network behind a different MAC address. This chain is applied to the packets leaving the router through a bridged interface dstnat-used for redirecting some packets to other destinations

You can put packet marks in bridge firewall (filter and NAT), which are the same as the packet marks in IP firewall configured by '/ip firewall mangle'. In this way, packet marks put by bridge firewall can be used in 'IP firewall', and vice versa.

General bridge firewall properties are described in this section. Some parameters that differ between nat and filter rules are described in further sections.

Sub-menu: /interface bridge filter, /interface bridge nat

Property Description

802.3-sap (integer; Default: ) DSAP (Destination Service Access Point) and SSAP (Source Service
Access Point) are 2 one-byte fields, which identify the network protocol entities which use the link-layer service. These bytes are always equal. Two hexadecimal digits may be specified here to match an SAP byte.

802.3-type (integer; Default: ) Ethernet protocol type, placed after the IEEE 802.2 frame header.
Works only if 802.3-sap is 0xAA (SNAP-Sub-Network Attachment Point header). For example, AppleTalk can be indicated by the SAP code of 0xAA followed by a SNAP type code of 0x809B.

action (accept | drop | jump | log | mark-packet | passthrough | return | set-Action to take if the packet is matched by the rule: priority; Default: ) accept-accept the packet. The packet is not passed to the next firewall rule drop-silently drop the packet jump-jump to the user-defined chain specified by the value of ju mp-target parameter log-add a message to the system log containing the following data: in-interface, out-interface, src-mac, protocol, src-ip:port- >dst-ip:port and length of the packet. After the packet is matched it is passed to the next rule in the list, similar as passthrough mark-packet-place a mark specified by the new-packet-mark parameter on a packet that matches the rule passthrough-if the packet is matched by the rule, increase counter and go to next rule (useful for statistics) return-passes control back to the chain from where the jump took place set-priority-set priority specified by the new-priority parameter on the packets sent out through a link that is capable of transporting priority (VLAN or WMM-enabled wireless interface). Read more

arp-dst-address (IP address; Default: ) ARP destination IP address.

arp-dst-mac-address (MAC address; Default: ) ARP destination MAC address.

arp-gratuitous (yes | no; Default: ) Matches ARP gratuitous packets.

arp-hardware-type (integer; Default: )1 ARP hardware type. This is normally Ethernet (Type 1).

arp-opcode (arp-nak | drarp-error | drarp-reply | drarp-request | inarp-reply ARP opcode (packet type) | inarp-request | reply | reply-reverse | request | request-reverse; Default: ) arp-nak-negative ARP reply (rarely used, mostly in ATM networks) drarp-error-Dynamic RARP error code, saying that an IP address for the given MAC address can not be allocated drarp-reply-Dynamic RARP reply, with a temporary IP address assignment for a host drarp-request-Dynamic RARP request to assign a temporary IP address for the given MAC address inarp-reply-InverseARP Reply inarp-request-InverseARP Request reply-standard ARP reply with a MAC address reply-reverse-reverse ARP (RARP) reply with an IP address assigned request-standard ARP request to a known IP address to find out unknown MAC address request-reverse-reverse ARP (RARP) request to a known MAC address to find out the unknown IP address (intended to be used by hosts to find out their own IP address, similarly to DHCP service)

arp-packet-type (integer 0..65535 | hex 0x0000-0xffff; Default: ) ARP Packet Type.

arp-src-address (IP address; Default: ) ARP source IP address.

arp-src-mac-address (MAC addres; Default: ) ARP source MAC address.

chain (text; Default: ) Bridge firewall chain, which the filter is functioning in (either a built-in one, or a user-defined one).

dst-address (IP address; Default: ) Destination IP address (only if MAC protocol is set to IP).

dst-address6 (IPv6 address; Default: ) Destination IPv6 address (only if MAC protocol is set to IPv6).

dst-mac-address (MAC address; Default: ) Destination MAC address.

dst-port (integer 0..65535; Default: ) Destination port number or range (only for TCP or UDP protocols).

in-bridge (name; Default: ) Bridge interface through which the packet is coming in.

in-bridge-list (name; Default: ) Set of bridge interfaces defined in interface list. Works the same as in -bridge.

in-interface (name; Default: ) Physical interface (i.e., bridge port) through which the packet is coming in.

in-interface-list (name; Default: ) Set of interfaces defined in interface list. Works the same as in- interface.

ingress-priority (integer 0..63; Default: ) Matches the priority of an ingress packet. Priority may be derived from VLAN, WMM, DSCP or MPLS EXP bit. read more

ip-protocol (dccp | ddp | egp | encap | etherip | ggp | gre | hmp | icmp | IP protocol (only if MAC protocol is set to IPv4) icmpv6 | idpr-cmtp | igmp | ipencap | ipip | ipsec-ah | ipsec-esp | ipv6 | ipv6- frag | ipv6-nonxt | ipv6-opts | ipv6-route | iso-tp4 | l2tp | ospf | pim | pup | dccp-Datagram Congestion Control Protocol rdp | rspf | rsvp | sctp | st | tcp | udp | udp-lite | vmtp | vrrp | xns-idp | xtp; ddp-Datagram Delivery Protocol Default: ) egp-Exterior Gateway Protocol encap-Encapsulation Header etherip-Ethernet-within-IP Encapsulation ggp-Gateway-to-Gateway Protocol gre-Generic Routing Encapsulation hmp-Host Monitoring Protocol icmp-IPv4 Internet Control Message Protocol icmpv6 - IPv6 Internet Control Message Protocol idpr-cmtp-Inter-Domain Policy Routing Control Message Transport Protocol igmp-Internet Group Management Protocol ipencap-IP in IP (encapsulation) ipip-IP-within-IP Encapsulation Protocol ipsec-ah-IPsec Authentication Header ipsec-esp-IPsec Encapsulating Security Payload ipv6 - Internet Protocol version 6 ipv6-frag-Fragment Header for IPv6 ipv6-nonxt-No Next Header for IPv6 ipv6-opts-Destination Options for IPv6 ipv6-route-Routing Header for IPv6 iso-tp4 - ISO Transport Protocol Class 4 l2tp-Layer Two Tunneling Protocol ospf-Open Shortest Path First pim-Protocol Independent Multicast pup-PARC Universal Packet rdp-Reliable Data Protocol rspf-Radio Shortest Path First rsvp-Reservation Protocol sctp-Stream Control Transmission Protocol st-Internet Stream Protocol tcp-Transmission Control Protocol udp-User Datagram Protocol udp-lite-Lightweight User Datagram Protocol

jump-target (name; Default: )

limit (integer/time,integer; Default: )

log (yes | no; Default: no)

log-prefix (text; Default: )

mac-protocol (802.2 | arp | capsman | dot1x | homeplug-av | ip | ipv6 | ipx | lacp | length | lldp | loop-protect | macsec | mpls-multicast | mpls-unicast | mvrp | packing-compr | packing-simple | pppoe | pppoe-discovery | rarp | romon | service-vlan | vlan | integer 0..65535 | hex 0x0000-0xffff; Default: )

new-packet-mark (string; Default: )

new-priority (integer | from-ingress; Default: )

out-bridge (name; Default: )

out-bridge-list (name; Default: )

out-interface (name; Default: )

out-interface-list (name; Default: )

vmtp-Versatile Message Transaction Protocol vrrp-Virtual Router Redundancy Protocol xns-idp-Xerox Network Systems Internet Datagram Protocol xtp-Xpress Transport Protocol

If action=jump specified, then specifies the user-defined firewall chain to process the packet.

Matches packets up to a limited rate. A rule using this matcher will match until this limit is reached.

count-maximum average packet rate, measured in packets per second (pps), unless followed by Time option time-specifies the time interval over which the packet rate is measured burst-number of packets to match in a burst

Add a message to the system log containing the following data: in- interface, out-interface, src-mac, dst-mac, eth-protocol, ip-protocol, src-ip:port->dst-ip:port, and length of the packet.

Defines the prefix to be printed before the logging information.

Ethernet payload type (MAC-level protocol). To match protocol type for VLAN encapsulated frames (0x8100 or 0x88a8), a vlan-encap prop erty should be used.

802.2 - 802.2 Frames (0x0004) arp-Address Resolution Protocol (0x0806) homeplug-av-HomePlug AV MME (0x88E1) ip-Internet Protocol version 4 (0x0800) ipv6 - Internet Protocol Version 6 (0x86DD) ipx-Internetwork Packet Exchange (0x8137) length-Packets with length field (0x0000-0x05DC) lldp-Link Layer Discovery Protocol (0x88CC) loop-protect-Loop Protect Protocol (0x9003) mpls-multicast-MPLS multicast (0x8848) mpls-unicast-MPLS unicast (0x8847) mvrp-Multiple VLAN Registration protocol (0x88F5) packing-compr-Encapsulated packets with compressed IP packing (0x9001) packing-simple-Encapsulated packets with simple IP packing (0 x9000) pppoe-PPPoE Session Stage (0x8864) pppoe-discovery-PPPoE Discovery Stage (0x8863) rarp-Reverse Address Resolution Protocol (0x8035) service-vlan-Provider Bridging (IEEE 802.1ad) & Shortest Path Bridging IEEE 802.1aq (0x88A8) vlan-VLAN-tagged frame (IEEE 802.1Q) and Shortest Path Bridging IEEE 802.1aq with NNI compatibility (0x8100)
Sets a new packet-mark value.

Sets a new priority for a packet. This can be the VLAN, WMM or MPLS EXP priority Read more. This property can also be used to set an internal priori

Outgoing bridge interface.

Set of bridge interfaces defined in interface list. Works the same as ou t-bridge.

Interface that the packet is leaving the bridge through.

Set of interfaces defined in interface list. Works the same as out- interface.

packet-mark (name; Default: ) Match packets with a certain packet mark.

packet-type (broadcast | host | multicast | other-host; Default: ) MAC frame type:

||broadcast-broadcast MAC packet|
|---|---|
||host-packet is destined to the bridge itself multicast-multicast MAC packet other-host-packet is destined to some other unicast address, not to the bridge itself|
|src-address (IP address; Default: )|Source IP address (only if MAC protocol is set to IPv4).|
|src-address6 (IPv6 address; Default: )|Source IPv6 address (only if MAC protocol is set to IPv6).|
|src-mac-address (MAC address; Default: )|Source MAC address.|
|src-port (integer 0..65535; Default: )|Source port number or range (only for TCP or UDP protocols).|
|stp-flags (topology-change | topology-change-ack; Default: )|The BPDU (Bridge Protocol Data Unit) flags. Bridge exchange configuration messages named BPDU periodically for preventing loops topology-change-topology change flag is set when a bridge detects port state change, to force all other bridges to drop their host tables and recalculate network topology topology-change-ack-topology change acknowledgment flag is sent in replies to the notification packets|
|stp-forward-delay (integer 0..65535; Default: )|Forward delay timer.|
|stp-hello-time (integer 0..65535; Default: )|STP hello packets time.|
|stp-max-age (integer 0..65535; Default: )|Maximal STP message age.|
|stp-msg-age (integer 0..65535; Default: )|STP message age.|
|stp-port (integer 0..65535; Default: )|STP port identifier.|
|stp-root-address (MAC address; Default: )|Root bridge MAC address.|
|stp-root-cost (integer 0..65535; Default: )|Root bridge cost.|
|stp-root-priority (integer 0..65535; Default: )|Root bridge priority.|
|stp-sender-address (MAC address; Default: )|STP message sender MAC address.|
|stp-sender-priority (integer 0..65535; Default: )|STP sender priority.|
|stp-type (config | tcn; Default: )|The BPDU type: config-configuration BPDU tcn-topology change notification|
|tls-host (string; Default: )|Allows matching https traffic based on TLS SNI hostname. Accepts GL OB syntax for wildcard matching. Note that matcher will not be able to match hostname if the TLS handshake frame is fragmented into multiple TCP segments (packets).|
|vlan-encap (802.2 | arp | ip | ipv6 | ipx | length | mpls-multicast | mpls-|Matches the MAC protocol type encapsulated in the VLAN frame.|
|unicast | pppoe | pppoe-discovery | rarp | vlan | integer 0..65535 | hex||
|0x0000-0xffff; Default: )||
|vlan-id (integer 0..4095; Default: )|Matches the VLAN identifier field.|
|vlan-priority (integer 0..7; Default: )|Matches the VLAN priority (priority code point)|
|Footnotes:||

STP matchers are only valid if the destination MAC address is 01:80:C2:00:00:00/FF:FF:FF:FF:FF:FF (Bridge Group address), also STP should be enabled.

ARP matchers are only valid if mac-protocol is arp or rarp

VLAN matchers are only valid for 0x8100 or 0x88a8 ethernet protocols

IP or IPv6 related matchers are only valid if mac-protocol is either set to ip or ipv6

802.3 matchers are only consulted if the actual frame is compliant with IEEE 802.2 and IEEE 802.3 standards. These matchers are ignored for other packets.
### Bridge Packet Filter

This section describes specific bridge filter options.

Sub-menu: /interface bridge filter

Property Description

action (accept | drop | jump | log | Action to take if the packet is matched by the rule: mark-packet | passthrough | return | set-priority; Default: accept) accept-accept the packet. No action, i.e., the packet is passed through without undertaking any action, and no more rules are processed in the relevant list/chain drop-silently drop the packet (without sending the ICMP reject message) jump-jump to the chain specified by the value of the jump-target argument log-add a message to the system log containing the following data: in-interface, out-interface, src- mac, dst-mac, eth-proto, protocol, src-ip:port->dst-ip:port and length of the packet. After packet is matched it is passed to the next rule in the list, similar as passthrough mark-mark the packet to use the mark later passthrough-ignore this rule and go on to the next one. Acts the same way as a disabled rule, except for the ability to count packets return-return to the previous chain, from where the jump took place set-priority-set priority specified by the new-priority parameter on the packets sent out through a link that is capable of transporting priority (VLAN or WMM-enabled wireless interface). Read more

### Bridge NAT

This section describes specific bridge NAT options.

Sub-menu: /interface bridge nat

Property Description

action (accept | drop | jump | mark-packet | redirect | set-Action to take if the packet is matched by the rule: priority | arp-reply | dst-nat | log | passthrough | return | src-nat; Default: accept) accept-accept the packet. No action, i.e., the packet is passed through without undertaking any action, and no more rules are processed in the relevant list/chain arp-reply-send a reply to an ARP request (any other packets will be ignored by this rule) with the specified MAC address (only valid in dstnat chain) drop-silently drop the packet (without sending the ICMP reject message) dst-nat-change destination MAC address of a packet (only valid in dstnat chain) jump-jump to the chain specified by the value of the jump-target argument log-log the packet mark-mark the packet to use the mark later passthrough-ignore this rule and go on to the next one. Acts the same way as a disabled rule, except for the ability to count packets redirect-redirect the packet to the bridge itself (only valid in dstnat chain) return-return to the previous chain, from where the jump took place set-priority-set priority specified by the new-priority parameter on the packets sent out through a link that is capable of transporting priority (VLAN or WMM- enabled wireless interface). Read more src-nat-change source MAC address of a packet (only valid in srcnat chain)

to-arp-reply-mac-address (MAC address; Default: ) Source MAC address to put in Ethernet frame and ARP payload, when action=arp- reply is selected

to-dst-mac-address (MAC address; Default: ) Destination MAC address to put in Ethernet frames, when action=dst-nat is selected

to-src-mac-address (MAC address; Default: ) Source MAC address to put in Ethernet frames, when action=src-nat is selected

## <u>See also</u>

CRS1xx/2xx series switches Marvell Prestera switch chip features Switch chip features MTU on RouterBOARD Layer2 misconfiguration Bridge VLAN Table
