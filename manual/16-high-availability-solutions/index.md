# High Availability Solutions

* [High Availability Solutions](high-availability-solutions.md) - High availability solutions in RouterOS provide redundancy and load-sharing designs including bonding, VRRP, multi-chassis link aggregation, and WAN load balancing to enhance service continuity and link resilience
* [Bonding](bonding.md) - Bonding allows combining multiple ethernet interfaces into a single virtual link for higher bandwidth and failover, with MikroTik RouterOS supporting various modes including LACP and hardware offloading for specific

## Load Balancing

* [Load Balancing](load-balancing.md) - Network load balancing in MikroTik RouterOS allows distributing traffic across multiple links without dynamic routing, with options for per-connection or per-packet methods. The documentation includes setup examples
* [Failover (WAN Backup)](failover-wan-backup.md) - This page explains how to configure failover for WAN connections using recursive routing in MikroTik RouterOS, detailing setup steps with basic and improved monitoring configurations for reliable link switching
* [Per connection classifier](per-connection-classifier.md) - Per connection classifier (PCC) in MikroTik RouterOS divides traffic into streams using IP header fields like source/destination addresses and ports to distribute connections across links, with hashing for load
* [Multi-chassis Link Aggregation Group](multi-chassis-link-aggregation-group.md) - MLAG in RouterOS enables physical redundancy by configuring LACP bonds across two devices, allowing the client to perceive a single connection while ensuring failover. It uses ICCP for peer communication, supports

## User Guides

* [Bonding Examples](bonding-examples.md) - This page demonstrates how to bond EoIP tunnels over two wireless links using MikroTik RouterOS, showing configuration steps for creating bonded interfaces and verifying traffic distribution across the links
* [VRRP Configuration Examples](vrrp-configuration-examples.md) - This page provides basic VRRP configuration examples for MikroTik RouterOS, demonstrating how to set up master-backup redundancy between two routers with IP address sharing and ARP table updates during failover
* [VRRP](vrrp.md) - This page describes the Virtual Router Redundancy Protocol (VRRP) in MikroTik RouterOS, explaining how it provides router redundancy through IPv4/IPv6 multicast communication and prioritized election among routers
