# Firewall and Quality of Service

* [Firewall and Quality of Service](firewall-and-quality-of-service.md) - This section provides an overview of RouterOS firewall capabilities including NAT, connection tracking, and QoS features for securing traffic, classifying packets, and managing bandwidth

## Firewall

* [Firewall](firewall.md) - MikroTik RouterOS firewall provides stateful and stateless packet filtering, NAT, and advanced traffic classification to secure network data flow and prevent unauthorized access. It includes filter/raw, mangle, and
* [Address lists](address-lists.md) - Address lists group IP addresses, prefixes, ranges and DNS names under one name for firewall rules. Entries can be static, added by rules with a timeout, or resolved from names
* [Common Firewall Matchers and Actions](common-firewall-matchers-and-actions.md) - This page explains MikroTik RouterOS firewall statistics and commands, detailing how to view matching stats for IPv4/IPv6 rules, reset counters, and lists common matchers like MAC addresses, interfaces, IP ranges,
* [Filter](filter.md) - Firewall filters in MikroTik RouterOS control packet flow by allowing or blocking traffic through predefined chains (input, forward, output) with options to accept specific services or drop malicious packets
* [Layer7](layer7.md) - Layer7 protocol inspection in MikroTik RouterOS searches for patterns in network traffic streams, collecting initial packet data to identify specific protocols. It requires careful configuration for bidirectional
* [Mangle](mangle.md) - Mangle in RouterOS marks packets for advanced processing using special marks, enabling features like queue trees and NAT. It modifies IP header fields and operates through five predefined chains (PREROUTING, INPUT,
* [NAT](nat.md) - NAT in MikroTik RouterOS enables IPv4 address translation between private and public networks, supporting both source NAT (masquerading) for hiding internal IPs and destination NAT for redirecting external traffic to
* [Packet Flow in RouterOS](packet-flow-in-routeros.md) - This page explains how data packets flow through MikroTik RouterOS, detailing the interaction between bridging, routing, MPLS decisions, and firewall chains. It includes diagrams illustrating packet processing stages
* [Connection tracking](connection-tracking.md) - Connection tracking in MikroTik RouterOS enables stateful firewall functionality by monitoring logical network connections, supporting NAT and various firewall features. It assigns packets to states like new,

## Queues

* [Queues](queues.md) - This page introduces MikroTik RouterOS queueing and bandwidth management, covering HTB, PCQ, burst behavior, and queue types for traffic shaping. It explains how to configure simple and advanced queues using
* [HTB (Hierarchical Token Bucket)](htb-hierarchical-token-bucket.md) - HTB (Hierarchical Token Bucket) is a queuing discipline in RouterOS for rate limiting and burst handling, using a token bucket algorithm to manage data rates with configurable capacity and limits
* [PCQ example](pcq-example.md) - Per Connection Queue (PCQ) is a RouterOS queuing method for equalizing bandwidth among users, with examples showing how to set download/upload limits using Queue Tree and Simple Queues
* [Queue Burst](queue-burst.md) - Queue Burst feature allows temporary bandwidth bursts beyond configured limits when average traffic stays below a threshold, using burst-limit and burst-time parameters to control the burst duration and size
* [Queue size](queue-size.md) - This page explains how to configure queue size limits in MikroTik RouterOS, detailing the impact of setting maximum packet counts on traffic shaping and scheduling. It includes examples comparing 100% shapers,

## Queues / Queue types

* [Queue types](queue-types.md) - Queue types in MikroTik RouterOS define queuing disciplines for managing packet flow, with options like BFIFO and PFIFO offering basic FIFO behavior, while advanced types such as CAKE and FQCoDel provide latency
* [CAKE](cake.md) - CAKE (Common Applications Kept Enhanced) is an advanced queue management algorithm for RouterOS that optimizes network traffic handling through bandwidth shaping, flow isolation, and RTT-based congestion control. It
* [PFIFO,BFIFO](pfifobfifo.md) - PFIFO and BFIFO are MikroTik RouterOS queue management strategies following FIFO principles, with PFIFO prioritizing packets by arrival order and BFIFO managing byte-based bandwidth allocation. Both ensure fairness
* [Kid Control](kid-control.md) - Kid Control is a RouterOS feature allowing parental control over LAN devices by setting daily internet access schedules, bandwidth limits, and device-specific restrictions through profiles and firewall rules
* [NAT-PMP](nat-pmp.md) - NAT-PMP lets LAN clients learn the router's external IPv4 address and request port mappings, so applications accept incoming connections behind NAT without manual port forwarding. Covers enabling the RouterOS NAT-PMP
* [UPnP](upnp.md) - Universal Plug and Play (UPnP) in RouterOS: an Internet Gateway Device service that lets LAN applications request port mappings. The router creates dynamic destination NAT rules for the requested ports. Covers

## User Guides

* [Firewall and QoS Case Studies](firewall-and-qos-case-studies.md) - This page presents practical case studies for configuring firewall and QoS rules in MikroTik RouterOS, covering brute-force prevention, DDoS protection, connection rate limiting, port knocking, and advanced firewall
* [SSH brute-force protection](ssh-brute-force-protection.md) - Protect an internet-facing SSH service on RouterOS with firewall rules that count new connections per source address and block a source that opens too many in a short time. Covers what to do before exposing SSH,
* [Building Advanced Firewall](building-advanced-firewall.md) - This page guides building an advanced firewall on MikroTik RouterOS by configuring interface lists, filtering rules for IPv4 and IPv6, accepting ICMP/DHCPv6 while blocking invalid addresses, and managing traffic
* [Connection rate](connection-rate.md) - Connection Rate is a MikroTik RouterOS firewall feature that monitors and filters traffic based on connection speed, using 'connection-bytes' and 'connection-rate' to detect high-speed connections for prioritization
* [DDoS protection](ddos-protection.md) - Limit denial-of-service attacks with RouterOS firewall rules: count new connections per source and destination with dst-limit, put pairs that exceed the rate on address lists and drop them in the raw table. Covers
* [Port knocking](port-knocking.md) - Port knocking keeps the management ports of a RouterOS router closed until a client connects to a secret sequence of ports; the firewall then adds the client to a trusted address list. Covers the knock rules in the
