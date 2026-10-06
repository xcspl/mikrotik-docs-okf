---
type: Reference
title: "Quality of Service"
description: "This document defines Quality of Service (QoS) usage in RouterOS based on Marvell Prestera switch chips."
timestamp: '2026-05-26'
status: active
tags: [routeros, mikrotik, networking]
resource: ~/Downloads/ROS-260526-1445-796.pdf
sources:
  - resource: https://manual.mikrotik.com/docs/introduction/
---

# Quality of Service

Overview QoS Changes in RouterOS v7.23 Configuration Change Summary QoS Terminology QoS Enhancements in new generation Marvell Prestera Switch Chips QoS Device Support Applications and Usage Examples Basic Configuration Example Dante RDMA over Converged Ethernet (RoCE) QoS Marking Understanding Map ranges Understanding Port, Profile, and Map relation QoS Marking via Switch Rules (ACL) QoS Enforcement Hardware Queues Hardware Resources Resource Saving (Previous Generation Devices) Traffic Prioritization Active Queue Management (AQM) Weighted Random Early Detection (WRED) Explicit Congestion Notification (ECN) Priority-based Flow Control (PFC) Property Reference Switch settings Port settings Port Stats Port Resources/Usage Port PFC Stats (Previous Generations) Port PFC Stats (New Generations) QoS Menu QoS Settings QoS Monitor QoS Profile QoS Mapping VLAN Map DSCP Map Transmission Manager Transmission Queue Scheduler Priority-based Flow Control (PFC)

## Overview

This document defines Quality of Service (QoS) usage in RouterOS based on Marvell Prestera switch chips.

QoS is a set of features in network switches that allow network administrators to prioritize traffic and allocate network resources to ensure that important data flows smoothly and with low latency.

The primary function of QoS in network switches is to manage network traffic in a way that meets the specific requirements of different types of network applications. For example, voice and video data require low latency and minimal packet loss to ensure high-quality communication, while file transfers and other data applications can tolerate higher levels of latency and packet loss.

QoS works by identifying the type of traffic flowing through the switch and assigning it a priority level based on its requirements. The switch can then use this information to alter packet headers and prioritize the flow of traffic, ensuring that higher-priority traffic is given preferential treatment over lower-priority traffic.

RouterOS v7.15+ is required to support all QoS features:

1. QoS Marking. QoS profile matching by ingress packet headers, then egress header alternation according to the assigned QoS profiles.
2. QoS Enforcement. Avoid or resolve congestion based on the assigned QoS profiles and traffic shaping.
3. QoS Policy. Assign QoS profiles via ACL rules.
4.

4. Active Queue Management: WRED (Weighted Random Early Detection), ECN notification, and processing, PFC (Priority-based Flow Control).
5. Traffic shaping.
### QoS Changes in RouterOS v7.23

RouterOS version 7.23 introduced significant changes in Quality of Service offloading, simplifying the configuration process and introducing "lossless" traffic classes. While hardware resources are finite, an active queue management with the help of ECN and/or PFC prevents packet loss if all parties support the features and are configured properly. Prior RouterOS versions supported ECN and PFC as well, but in v7.23, the configuration process was streamlined.

Not all devices support lossless traffic. Check the QoS Device Support table.

Configuration Change Summary

QoS Settings: most changes were set to "auto" by default, allowing RouterOS to pick the best known settings for the setup. QoS Settings: added lossless-traffic-class and lossless-buffers, allowing explicit specification of lossless traffic and the reservation of queue resources for it. The user can leave those fields to "auto" as well. QoS Monitor: displays the shared pool usage for lossy and lossless separately. Tx Queue: removed shared pool index. Router OS automatically selects the shared pool based on the traffic type (lossy or lossless). QoS Profile: added automapping to the specified PCP and DSCP values (enabled by default). For example, adding a QoS profile with DSCP=46 automatically applies the profile to traffic received from trusted ports.

## QoS Terminology

These terms will be used throughout the article.

QoS-Quality of Service. ACL-Access Control List, a set of switch rules used to filter network traffic based on specified criteria. AQM-Active Queue Management. DSCP-Differentiated Services Code Point, a 6-bit field in the IP header used to prioritize network traffic. ECN-Explicit Congestion Notification. ETS-Enhanced Transmission Selection. PCP-Priority Code Point, a 3-bit field in the VLAN header used to prioritize traffic within a VLAN. PFC-Priority-based Flow Control (IEEE 802.1Qbb). RoCE-RDMA over Converged Ethernet. WRED-Weighted Random Early Detection. **/in/eth/sw/** a shortcut for **/interface/ethernet/switch/**. The shortcut works in CLI, too.

## QoS Enhancements in new generation Marvell Prestera Switch Chips

MikroTik devices with new generation Marvell Prestera switch chips (e.g. CRS8xx series running the switch-marvell package) offer a new approach in QoS enforcement. Previous models required making a tradeoff between guaranteed and shared Tx queue buffers. By increasing the shared buffer percentage, the device can absorb larger traffic bursts, but at the same time, one congested port can occupy all shared buffers, limiting the QoS capabilities of other ports. Using the new generation switch chips enable the best of both worlds by introducing Dynamic Buffers. A switch chip dynamically adjusts port and queue buffer limits based on the current congestion level. If there is no congestion within the device, a single port can absorb a large burst of traffic, preventing packet loss. When the Tx queue size increases across multiple ports, the device reduces per-port and per-queue limits, enforcing fair use of shared resources while ensuring enough buffers for non-congested queues to continue forwarding traffic. The entire process is automated, requiring zero configuration from the user.

Another improvement in new generation Marvell Prestera switch chips is eliminating the shortage of enqueued packet descriptors for storing control data. Previous generation devices had Packet Cap and Use stats. When a device received a burst of small packets, it could start tail-dropping packets due to hitting Packet Cap, even though it had enough queue buffers to store the payload. New generation devices ensure there is always enough memory to store control data, leaving the Dynamic Buffer size as the only limiting factor. That's why there are no Packet Cap/Use stats in new generation devices.

New generation devices require QoS HW Offloading to be enabled at all times (qos-hw-offloading=yes). RouterOS ignores user requests to disable it while keeping the field for backward compatibility.

## QoS Device Support

|Switch Chip|Models|QoS Profiles|QoS Maps|Tx Managers|WRED|ECN|PFC|Lossless Buffers|Dynamic Buffers|Port/Queue Usage Stats|
|---|---|---|---|---|---|---|---|---|---|---|
|98DX3236|CRS305-1G-4S+IN CRS326-24G-2S+ (RM/IN) CRS328-24P-4S+RM CRS328-4C-20S-4S+RM|128|1|8||||||Current values|
|98DX226S|CRS305-1G-4S+OUT (FiberBox Plus) CRS310-1G-5S-4S+ (netFiber 9/IN) CRS310-8G+2S+IN CRS318-16P-2S+OUT (netPower 16P) CRS320-8P-8B-4S+RM CRS418-8P-8G-2S+RM CRS418-8P-8G-2S+5axQ2axQ-RM|128|1|8||||||Current values|
|98DX224S|CRS318-1Fi-15Fr-2S-OUT (netPower 15FR)|128|1|8||||||Current values|
|98DX2528|CRS304-4XG-IN|128|1|8||||||Current values|
|98DX8525|CCR2216-1G-12XS-2XQ CRS518-16XS-2XQ-RM|1024|12|15|✔|✔|✔|✔||Max fill 1|
|98DX4310|CRS504-4XQ (IN/OUT) CRS510-8XS-2XQ-IN RDS2216-2XG-4S+4XS-2XQ|1024|12|15|✔|✔|✔|✔||Max fill 1|
|98DX8208|CRS309-1G-8S+IN|1024|12|15|✔|✔|✔|✔||Current values 2|
|98DX8212|CRS312-4C+8XG-RM|1024|12|15|✔|✔|✔|✔||Current values 2|
|98DX8216|CRS317-1G-16S+RM|1024|12|15|✔|✔|✔|✔||Current values 2|
|98DX8332|CRS326-24S+2Q+RM CRS326-4C+20G+2Q+RM|1024|12|15|✔|✔|✔|✔||Current values 2|
|98DX3257|CRS354-48G-4S+2Q+RM CRS354-48P-4S+2Q+RM|1024|12|15|✔|✔|✔|✔||Current values 2|
|98DX3255|CCR2116-12G-4S+|1024|12|15|✔|✔|✔|✔||Current values 2|
|98CX8410|CRS520-4XS-16XQ-RM|1024|12|15|✔|✔|✔|✔||Unavailable 3|
|98DX7335 1 2 3 2S+ device where:|CRS812-8DS-2DQ-2DDQ-RM CRS804-4DDQ-hRM Applications and Usage Examples Basic Configuration Example all ports are bridged and using vlan-filtering; sfp-sfpplus1 is a VLAN trunk connected to another switch;|1024|12 Due to hardware limitations, some switch chip models may break traffic flow while accessing QoS port/queue usage data. Usage data for individual queues on a port are unavailable, only the total usage for the entire port can be accessed.|15 The device gathers max queue fill statistics instead of displaying the current usage values. Use the reset-counters command to reset those stats. In this example, we define just one QoS level-VoIP (IP Telephony) on top of the standard "Best Effort" class. Let's imagine that we have a CRS326-24G-|✔|✔|✔|✔|✔|Current values + Max fill|

ether1-ether9 are dedicated ports for IP phones; ether10-ether24 are standard ports for host connection;

First, we need to define QoS profiles. Defined dscp and pcp values that will be used in forwarded packets on egress:

/interface ethernet switch qos profile add dscp=46 name=voip pcp=5 traffic-class=5

Port-based QoS profile assignment on dedicated ports for IP phones applies to ingress traffic. Other Ethernet ports will use the default profile (where ds cp=0 and pcp=0):

/interface ethernet switch qos port set ether1 profile=voip set ether2 profile=voip set ether3 profile=voip set ether4 profile=voip set ether5 profile=voip set ether6 profile=voip set ether7 profile=voip set ether8 profile=voip set ether9 profile=voip

trust-l3 and The trunk port receives both types of QoS traffic, we need to enable trust-l2 to differentiate them:

/interface ethernet switch qos port set sfp-sfpplus1 trust-l3=trust trust-l2=trust

If you are running RouterOS version 7.23 or later, the VLAN priority and IP DSCP mapping is created automatically, so this step is not required. If you are using an earlier RouterOS version, you must manually create the VLAN priority and IP DSCP mapping with the QoS profile:

/interface ethernet switch qos map ip add dscp=46 profile=voip

/interface ethernet switch qos map vlan add pcp=5 profile=voip

Finally, enable QoS hardware offloading for the above settings to start working:

/interface ethernet switch set switch1 qos-hw-offloading=yes

It is possible to verify the port QoS settings with print command:

[admin@MikroTik] /interface/ethernet/switch/qos/port print Columns: NAME, SWITCH, PROFILE, MAP, TRUST-L2, TRUST-L3 # NAME SWITCH PROFILE MAP TRUST-L2 TRUST-L3 TX-MANAGER 0 ether1 switch1 voip default ignore ignore default 1 ether2 switch1 voip default ignore ignore default 2 ether3 switch1 voip default ignore ignore default 3 ether4 switch1 voip default ignore ignore default 4 ether5 switch1 voip default ignore ignore default 5 ether6 switch1 voip default ignore ignore default 6 ether7 switch1 voip default ignore ignore default 7 ether8 switch1 voip default ignore ignore default 8 ether9 switch1 voip default ignore ignore default 9 ether10 switch1 default default ignore ignore default 10 ether11 switch1 default default ignore ignore default 11 ether12 switch1 default default ignore ignore default 12 ether13 switch1 default default ignore ignore default 13 ether14 switch1 default default ignore ignore default 14 ether15 switch1 default default ignore ignore default 15 ether16 switch1 default default ignore ignore default 16 ether17 switch1 default default ignore ignore default 17 ether18 switch1 default default ignore ignore default 18 ether19 switch1 default default ignore ignore default 19 ether20 switch1 default default ignore ignore default 20 ether21 switch1 default default ignore ignore default 21 ether22 switch1 default default ignore ignore default 22 ether23 switch1 default default ignore ignore default 23 ether24 switch1 default default ignore ignore default 24 sfp-sfpplus1 switch1 default default trust ignore default 25 sfp-sfpplus2 switch1 default default ignore ignore default 26 switch1-cpu switch1

Now incoming packets on ports ether1-ether9 are marked with a Priority Code Point (PCP) value of 5 and a Differentiated Services Code Point (DSCP) value of 46, and incoming packets on ports ether10-ether24 are marked with PCP and DSCP values of 0. When packets are incoming to sfp-sfpplus1 port, any packets with a PCP value of 5 will retain their PCP value of 5 and DSCP value of 46, while all other packets will be marked with PCP and DSCP values of 0.

Dante

Starting from RouterOS v7.15, all MikroTik QoS-Capable devices are compatible with Dante.

Dante hardware use the following DSCP / Diffserv priority values for traffic prioritization.

|Dante Priority|Usage|DSCP Label|DSCP Value|
|---|---|---|---|
|High|Time critical PTP events|CS7|56|
|Medium|Audio, PTP|EF|46|
|None The example assumes that the switch is using its default configuration, which includes a default "bridge" interface and all Ethernet interfaces added as bridge ports, and any of these interfaces could be used for Dante. First, create QoS Profiles to match Dante traffic classes, there is already a pre-existing "default" profile that corresponds to Dante's None priority. /interface/ethernet/switch/qos/profile add name=dante-ptp dscp=56 pcp=7 traffic-class=7 add name=dante-audio dscp=46 pcp=5 traffic-class=5|Other traffic|BE|0|

If you are running RouterOS version 7.23 or later, the IP DSCP mapping is created automatically, so this step is not required. If you are using an earlier RouterOS version, create a QoS mapping to match QoS profiles based on DSCP values.

/interface/ethernet/switch/qos/map/ip add dscp=56 profile=dante-ptp add dscp=46 profile=dante-audio

Configure hardware queues to enforce QoS on Dante traffic.

/interface/ethernet/switch/qos/tx-manager/queue set [find where traffic-class=7] schedule=strict-priority set [find where traffic-class=5] schedule=strict-priority

Dante's High and Medium priority traffic is scheduled in strict order. The devices transmit time-critical PTP packets until queue7 gets empty, then proceed with audio (queue5). Other traffic gets transmitted only when PTP and audio queues are empty.

The next step is to enable trust mode for incoming Layer3 packets (IP DSCP field):

/interface/ethernet/switch/qos/port set [find] trust-l3=keep

Finally, enable QoS hardware offloading for the above settings to start working:

/interface ethernet switch set switch1 qos-hw-offloading=yes

When using Dante in multicast mode, it is beneficial to enable IGMP snooping on the switch. This feature directs traffic only to ports with subscribed devices, preventing unnecessary flooding. Additionally, enabling an IGMP querier (if not already enabled on another device in the same LAN), adjusting query intervals, and activating fast-leave can further optimize multicast performance.

/interface/bridge set [find name=bridge] igmp-snooping=yes multicast-querier=yes query-interval=60s

/interface/bridge/port set [find] fast-leave=yes

### RDMA over Converged Ethernet (RoCE)

RoCE allows you to directly access memory on remote storage systems using Ethernet networks without involving the host CPU. This capability significantly reduces latency and CPU overhead, making RoCE ideal for high-performance computing and data center environments. RoCE also enables a converged network, where various services (such as data storage, networking, and multimedia) run over a single Ethernet infrastructure. This simplifies network management and reduces the cost and complexity of maintaining separate networks.

RoCE achieves this through the use of ECN and PFC mechanisms. These features help prevent network congestion and packet loss, ensuring reliable, lossless communication. See the device feature table for compatible switches. Although switches can support RoCE environments, the end hosts must also be compatible with the RoCE protocol and equipped with RDMA-capable network interface cards (NICs).

There are two main versions of RoCE. RoCEv1 operates as an Ethernet link layer protocol and uses Ethertype 0x8915. RoCEv2 works over standard IP networks, using UDP destination port number 4791. ECN bits in the IP header are marked to signal network congestion, and a Congestion Notification Packet (CNP) is used to acknowledge congestion to the sender. For traffic prioritization, DSCP 26 is used for RoCEv2 traffic, while DSCP 48 for CNPs.

The following example can be used for lossless RoCEv2 with PFC and ECN and it assumes that the switch is using its default configuration, which includes a default "bridge" interface and all Ethernet interfaces added as bridge ports. The minimal recommended RouterOS version is 7.17.

First, configure additional profiles. Non-RoCE traffic will be assigned to already existing "default" profile with traffic-class 1, RoCEv2 to traffic-class 3, and CNP to traffic-class 6.

/interface ethernet switch qos profile add dscp=26 name=roce traffic-class=3 add dscp=48 name=cnp traffic-class=6

If you are running RouterOS version 7.23 or later, the IP DSCP mapping is created automatically, so this step is not required. If you are using an earlier RouterOS version, create a QoS mapping to match QoS profiles based on DSCP values.

/interface ethernet switch qos map ip add dscp=26 profile=roce add dscp=48 profile=cnp

Configure hardware queues and scheduler. We are using ETS (schedule=high-priority-group) for traffic-class 1 and traffic-class 3 with 50% bandwith assigment each (weight=1), and strict priority scheduling for traffic-class 6. Additionally, enable ECN (ecn=yes) for traffic-class 3 to mark IP packets in the switch that experience congestion.

/interface ethernet switch qos tx-manager queue set 1 schedule=high-priority-group weight=1 set 3 schedule=high-priority-group weight=1 ecn=yes set 6 schedule=strict-priority

Although using schedule=low-priority-group allows you to create separate ETS scheduling and bandwidth allocation for a different set of traffic-classes, it is not recommended to use this setting together with lldp-dcbx=yes. The reason is that the ETS Configuration /Recommendation TLVs are designed to handle a single bandwidth allocation across traffic classes, thus schedule=high-priority-group should be used instead.

Configure PFC profile for traffic-class 3 to ensure a lossless environment for RoCEv2 traffic.

/interface ethernet switch qos priority-flow-control add name=pfc-tc3 rx=yes traffic-class=3 tx=yes

Set Layer3 trust mode (trust-l3=keep) on switch ports where RoCEv2 traffic is expected, set PFC (pfc=pfc-tc3) and egress-rate for queue3 to comply with PFC requirements (egress-rate-queue3=10.0Gbps). In this example, 10Gbps SFP+ interfaces are used, and the egress rate can be set to match the physical speed of the interface. Change this property depending on your interface speeds.

/interface ethernet switch qos port set sfp-sfpplus1 egress-rate-queue3=10.0Gbps pfc=pfc-tc3 trust-l3=keep set sfp-sfpplus2 egress-rate-queue3=10.0Gbps pfc=pfc-tc3 trust-l3=keep set sfp-sfpplus3 egress-rate-queue3=10.0Gbps pfc=pfc-tc3 trust-l3=keep set sfp-sfpplus4 egress-rate-queue3=10.0Gbps pfc=pfc-tc3 trust-l3=keep

Enable QoS hardware offloading for the above settings to start working.

/interface ethernet switch set switch1 qos-hw-offloading=yes

Enable the LLDP Data Center Bridging Capability Exchange Protocol (DCBX) to share QoS settings and capabilities with other neighboring devices.

/ip neighbor discovery-settings set lldp-dcbx=yes

As an optional step, increase the L2MTU to accommodate larger data packets.

/interface ethernet set [find switch=switch1] l2mtu=9500

## QoS Marking

||Profile mapping.|Understanding Map ranges In order to avoid defining all possible PCP and DSCP mappings, RouterOS allows setting multiple values and ranges for PCP and DSCP values for QoS In the following example, PCP values 0 and 2 use the default QoS profile, 1, 3-4 - streaming, 5 - voip, and 6-7 - control.|
|---|---|---|
||add pcp=5 profile=voip|/interface ethernet switch qos map vlan add pcp=1,3-4 profile=streaming add pcp=6-7 profile=control Understanding Port, Profile, and Map relation Each switch port has Layer2 and Layer3 trust settings that will change how ingress packets are classified into QoS profiles and what PCP and DSCP values will be used. Below are tables that describe all possible options:|
|qos- trust- l2|qos- trust- l3|Behavior|
|ignore ignore ignore trust trust trust keep keep keep|ignore trust keep ignore trust keep ignore trust keep|The port is considered untrusted. Both headers are ignored, and the port's profile is forced to all ingress packets. This is the default setting. Trust the Layer 3 header. Use the DSCP field from the IP header of ingress packets for QoS profile lookup (see /in/eth/sw/qos /map/ip). If the lookup fails (no QoS profiles are mapped to the given DSCP value), the default QoS profile is used (not the switch port's QoS profile). The switch port's profile field is used only for non-IP traffic. Trust the Layer 3 header. Use the DSCP field from the IP header of ingress packets for QoS profile lookup (see /in/eth/sw/qos /map/ip). If the lookup fails, the default QoS profile is used. The switch port's profile field is used only for non-IP traffic. If the forwarded/routed packet is VLAN-tagged, its PCP value is set from the selected QoS profile. However, the original DSCP value of the packet is kept intact. Trust the Layer 2 header, but ignore L3. If an ingress packet is VLAN-tagged, use the PCP field from the VLAN header for QoS profile lookup (see /in/eth/sw/qos/map/vlan). If the lookup fails (no QoS profiles are mapped to the given PCP value), the defa ult QoS profile is used. The switch port's profile field is used only for untagged traffic. Trust both headers, but Layer 3 has higher precedence. In the case of an IP packet, use the DSCP field for QoS profile lookup (see / in/eth/sw/qos/map/ip). If the DSCP-to-QoS lookup fails, use the default profile. If the packet is not an IP packet but is VLAN- tagged, use the PCP field from the VLAN header for QoS profile lookup (see /in/eth/sw/qos/map/vlan).  If the VLAN-to-QoS lookup fails, use the default QoS profile. Non-IP untagged packets use the switch port's profile. The same as trust+trust, but the original DSCP value is preserved in forwarded/routed packets. Trust the Layer 2 header but ignore L3. If an ingress packet is VLAN-tagged, use the PCP field from the VLAN header for QoS profile lookup (see /in/eth/sw/qos/map/vlan). If the lookup fails (no QoS profiles are mapped to the given PCP value), the defa ult QoS profile is used. The switch port's profile field is used only for untagged traffic. If the packet is VLAN-tagged on both ingress and egress, the original PCP value is kept. Trust both headers, but Layer 3 has higher precedence. In the case of an IP packet, use the DSCP field for QoS profile lookup (see / in/eth/sw/qos/map/ip). If the DSCP-to-QoS lookup fails, use the default profile. If the packet is not an IP packet but is VLAN- tagged, use the PCP field from the VLAN header for QoS profile lookup (see /in/eth/sw/qos/map/vlan).  If the VLAN-to-QoS lookup fails, use the default QoS profile. Non-IP untagged packets use the switch port's profile. If the packet is VLAN-tagged on both ingress and egress, the original PCP value is kept. The DSCP value in forwarded/routed packets is set from the selected QoS profile. Trust both headers, but Layer 3 has higher precedence. In the case of an IP packet, use the DSCP field for QoS profile lookup (see / in/eth/sw/qos/map/ip). If the DSCP-to-QoS lookup fails, use the default profile. If the packet is not an IP packet but is VLAN- tagged, use the PCP field from the VLAN header for QoS profile lookup (see /in/eth/sw/qos/map/vlan).  If the VLAN-to-QoS lookup fails, use the default QoS profile. Non-IP untagged packets use the switch port's profile. Keep both the original PCP and/or DSCP values intact in cases of VLAN-tagged and/or IP packets, respectively.|
||Port settings|The selected QoS profile and the source for PCP / DSCP field values in forwarded/routed packets|
|qos-trust-l2||qos-trust-l3 VLAN-Tagged IP Untagged IP VLAN-Tagged Non-IP Untagged Non-IP|

|||QoS Profile|PCP|DSCP|QoS Profile|PCP 1|DSCP|QoS Profile|PCP|DSCP|QoS Profile|PCP 1|DSCP|
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
|ignore|ignore|profile|profile|profile|profile|profile|profile|profile|profile|-|profile|profile|-|
|ignore|trust|map/ip|map/ip|map/ip|map/ip|map/ip|map/ip|profile|profile|-|profile|profile|-|
|ignore|keep|map/ip|map/ip|original|map/ip|map/ip|original|profile|profile|-|profile|profile|-|
|trust|ignore|map/vlan|map/vlan|map/vlan|profile|profile|profile|map/vlan|map/vlan|-|profile|profile|-|
|trust|trust|map/ip|map/ip|map/ip|map/ip|map/ip|map/ip|map/vlan|map/vlan|-|profile|profile|-|
|trust|keep|map/ip|map/ip|original|map/ip|map/ip|original|map/vlan|map/vlan|-|profile|profile|-|
|keep|ignore|map/vlan|original|map/vlan|profile|profile|profile|map/vlan|original|-|profile|profile|-|
|keep|trust|map/ip|original|map/ip|map/ip|profile|map/ip|map/vlan|original|-|profile|profile|-|
|keep|keep|map/ip|original|original|map/ip|profile|original|map/vlan|original|-|profile|profile|-|

1 applies only when ingress traffic is untagged, but the egress needs to be VLAN-tagged.

### QoS Marking via Switch Rules (ACL)

Starting from RouterOS v7.15, it is possible to assign QoS profiles via Switch Rules (ACL).

Sub-menu: /interface/ethernet/switch/rule

New/Changed Description Properties

new-qos-profile (name) The name of the QoS profile to assign to the matched packets.

keep-qos-fields (yes | no; Should the original values of QoS fields (PCP, DSCP) be kept (yes), or replace them with the ones from the assigned QoS Default: no) profile (no)? Relevant only if new-qos-profile is set.

new-vlan-priority (0..7) Deprecated and should be replaced with the respective new-qos-profile. Kept for backward compatibility. Relevant only if qos-hw-offloading=no.

The following example assigns a QoS profile based on the source MAC address.

/interface ethernet switch rule add new-qos-profile=stream ports=ether1,ether2 src-mac-address=00:01:02:00:00:00/FF:FF:FF:00:00:00 switch=switch1 add new-qos-profile=voip ports=ether1,ether2 src-mac-address=04:05:06:00:00:00/FF:FF:FF:00:00:00 switch=switch1

## QoS Enforcement

### Hardware Queues

Each switch port has eight hardware transmission (tx) queues (queue0..queue7). Each queue corresponds to a traffic class (tc0..tc7) set by a QoS profile. Each ingress packet gets assigned to a QoS profile, which, in turn, determines the traffic class for tx queue selection on the egress port.

Hardware queues are of variable size-set by the Transmission Manager. Moreover, multiple ports and/or queues can share resources with each other (so- called Shared Buffers). For example, a device with 25 ports has memory (buffers) to queue 1200 packets in total. If we split the resources equally, each port gets 48 exclusive buffers with a maximum of 6 packets per queue (48/8) - which is usually insufficient to absorb even a short burst of traffic. However, choosing to share 50% of the buffers leaves each port with 24 exclusive buffers (3 per queue), but at the same time, a single queue can grow up to 603 buffers (3 exclusive + 600 shared).

RouterOS allows enabling/disabling the shared pool for each queue individually-for example, to prevent low-priority traffic from consuming the entire hardware memory. In addition, port buffer limits may prevent a single low-speed port from consuming the entire shared pool. See QoS Settings and  Trans mission Manager for details.

The default, best-effort (PCP=0, DSCP=0) traffic class is 1, while the lowest priority (PCP=1) has traffic class 0.

### Hardware Resources

The hardware (switch chips) has limited resources (memory). There are two main hardware resources that are relevant to QoS:

Packet descriptors-contain packet control information (target port, header alternation, etc). Data buffers-memory chunks containing the actual payload. Buffer size depends on the switch chip model. Usually - 256 bytes.

One packet descriptor may use multiple buffers (depending on the payload size); buffers may be shared by multiple descriptors-in cases of multicast /broadcast. If the hardware does not have enough free descriptors or buffers, the packet gets dropped (tail-drop).

Hardware resources can be limited per destination type (multicast/unicast), per port, and per each tx queue. If any limits are reached, no more packets can be enqueued for transmission, and further packets get dropped.

RouterOS obscures low-level hardware information, allowing to set resource limits either in terms of packets or a percentage of the total amount. RouterOS automatically calculates the required hardware descriptor and buffer count based on the user-specified packet limit and port's MTU. Moreover, RouterOS comes with preconfigured hardware resources, so there is no need to do a manual configuration in common QoS environments.

Changing any hardware resource allocation parameter in runtime results in a temporary device halt when no packets can be enqueued nor transmitted. Temporary packet loss is expected while the device is forwarding traffic.

### Resource Saving (Previous Generation Devices)

This section does not apply to devices that support Dynamic Buffers.

Since reallocating hardware resources in runtime is not an option, RouterOS cannot automatically free queue buffers reserved for inactive ports. Those buffers remain unused. However, if the user knows that the specific ports will never be used (e.g., stay physically disconnected), the respective queue resources can be manually freed by using the built-in "offline" tx-manager with minimum resources, for example:

/interface/ethernet/switch/qos/port set sfp-sfpplus1 tx-manager=offline set sfp-sfpplus2 tx-manager=offline

Avoid configuring the "offline" tx-manager on switch-cpu port.

When configuring tx-manager setting to QSFP+ or QSFP28 interfaces, you must apply the same configuration to all four sub-interfaces of a port. For example, if the interface qsfp28-1-1 is active and linked at 100Gbps, while sub-interfaces (qsfp28-1-2, qsfp28-1-3, qsfp28-1-4) are showing a non-running flag, do not assign the "offline" tx-manager to thouse non-running sub-interfaces. Doing so will impact the 100Gbps link as well. However, if none of the four sub-interfaces are running, it is safe to assign the "offline" tx-manager setting.

## Traffic Prioritization

The hardware provides two types of traffic transmission prioritization:

Strict Priority-traffic from higher queues is always transmitted first; Enhanced Transmission Selection (ETS) - multiple queues participate in packet transmission scheduling at the same time.

Strict priority queues are straightforward. If the highest priority queue (Q7) has packets, those are transmitted first. When Q7 is empty, packets from Q6 get transmitted, and so on. The packets from the lowest priority queue (Q0) are transmitted only if all other queues are empty.

The downside of strict prioritization is increased latency in lower queues while "overprioritizing" higher queues. Suppose the acceptable latency of TC5 is 20ms, TC3 - 50ms. Traffic appearing in Q5 gets immediately transmitted due to the strict priority of the queue, adding extra latency to every packet in the lower queues (Q4..Q0). A packet burst in Q5 (e.g., a start of a voice call) may temporarily "paralyze" Q3, increasing TC3 latencies over the acceptable 50ms (or even causing packet drops due to full queue) while TC5 packets get transmitted at <1ms (way below the 20ms limit). Slightly sacrificing TC5 latency by transmitting TC3 packets in between would make everybody happy. That ETS is for.

Enhanced Transmission Selection (ETS) schedule traffic for transmission from multiple queues (group members) in a weighted round-robin manner. A queue's weight sets the number of packets transmitted from the queue in each round. For example, if Q2, Q1, and Q0 are the group members, and their weights are 3, 2, and 1, respectively, the scheduler transmits 3 packets from Q2, 2 - from Q1, and 1 - from Q0. The actual Tx order is "Q2, Q1, Q0, Q2, Q1, Q2" - for even fairer scheduling.

There are two hardware groups: low-priority-group and high-priority-group. There is a strict priority ordering between the two groups: the low- priority-group is transmitting only when all queues in the high-priority-group are empty. However, it is possible to use only one group for all queues.

The default (built-in) RouterOS queue setup is listed below. Q3-Q5 share the bandwidth within the high-priority group, where packets are transmitted while Q6 and Q7 are empty. Q0-Q2 are the members of the low-priority-group, where packets are transmitted while Q3-Q7 are empty.

[admin@MikroTik] /interface/ethernet/switch/qos/tx-manager/queue> print Columns: TX-MANAGER, TRAFFIC-CLASS, SCHEDULE, WEIGHT, QUEUE-BUFFERS, USE-SHARED-BUFFERS # TX-MANAGER TRAFFIC-CLASS SCHEDULE WEIGHT QUEUE-BUFFERS USE-SHARED-BUFFERS 0 default 0 low-priority-group 1 auto no 1 default 1 low-priority-group 2 auto yes 2 default 2 low-priority-group 3 auto yes 3 default 3 high-priority-group 3 auto yes 4 default 4 high-priority-group 4 auto yes 5 default 5 high-priority-group 5 auto yes 6 default 6 strict-priority auto yes 7 default 7 strict-priority auto yes

It is recommended that all group members are adjacent to each other.

## Active Queue Management (AQM)

### Weighted Random Early Detection (WRED)

WRED is a per-queue congestion control mechanism that signals congestion events to the end-points by dropping packets. WRED relies on the existence of rate throttling mechanisms in the end-points that react to packet loss, such as TCP/IP. WRED uses a randomized packet drop algorithm in an attempt to anticipate congestion events and respond to them by throttling traffic rates before the congestion actually happens. The randomness property of WRED prevents throughput collapse related to the global synchronization of TCP flows.

WRED can be enabled/disabled per each queue in each Tx Manager. Disable WRED for lossless traffic! Also, there is no reason to enable WRED on high- speed ports where congestion should not happen in the first place.

The behavior is controlled via WRED threshold. WRED threshold is the maximum number of packets/bytes that can exceed the queue shared buffer limit (cap). A random packet drop begins when queue usage exceeds their respective capacities:

queueX-packet-use > queueX-shared-packet-cap or queueX-byte-use > queueX-shared-byte-cap.

The more usage exceeds capacity, the higher the packet drop chance, reaching 100% at queueX-shared-packet-cap + wred-packet-threshold (or byte).

RouterOS automatically chooses the actual WRED threshold values according to queue or shared pool capacities. The user may shift the thresholds in one way or another via QoS Settings.

WRED requires the respective Tx queues to use shared buffers (use-shared-buffers=yes).

Choosing a WRED threshold value is a tradeoff between congestion anticipation and burst absorption. Setting a higher WRED threshold may lead to earlier traffic rate throttling and, therefore, resolve congestion. On the other hand, a high threshold leads to packet drops in limited traffic bursts that could be absorbed by the queue buffers and transformed losslessly if WRED didn't kick in. For instance, initiating a remote database connection usually starts with heavier traffic ("packet burst") at the initialization phase; then, the traffic rate drops down to a "reasonable" level. Any packet drop during the initialization phase leads to nothing but a slower database connection due to the need for retransmission. Hence, lowering the WRED threshold or entirely disabling WRED on such traffic is advised. The opposite case is video streaming. Early congestion detection helps select a comfortable streaming rate without losing too much bandwidth on retransmission or/and "overshooting" by sacrificing the quality level by too much.

Use Switch Rules (ACL) or other QoS Marking techniques to differentiate traffic and put packets into queues with desired WRED settings.

The following script only applies WRED to TCP/IP traffic by redirecting it to queue2. UDP and other packets are left in queue1 - since their end-points usually cannot respond to early drops. Queue1 and queue2 are scheduled equally-without prioritizing one queue over another.

/interface/ethernet/switch/qos/profile add name=tcp-wred traffic-class=2 pcp=0 dscp=0

# move TCP traffic to queue2 /interface/ethernet/switch/rule add new-qos-profile=tcp-wred ports=ether1,ether2,ether3,ether4 protocol=tcp switch=switch1

# set the same scheduling priority (weight) between queue1 and queue2 # apply WRED only to queue2 - TCP traffic /interface/ethernet/switch/qos/tx-manager/queue/ set [find where traffic-class=1] weight=2 schedule=low-priority-group use-shared-buffers=yes wred=no set [find where traffic-class=2] weight=2 schedule=low-priority-group use-shared-buffers=yes wred=yes

### (ECN)Explicit Congestion Notification

Some switch chips can perform ECN marking of IP packets on the hardware level, according to RFC 3168. Hardware ECN marking is based on the WRED mechanism, but instead of dropping IP packets, they are marked with CE (Congestion Experienced, binary 11) in the ECN field (two least significant bits in IPv4/TOS or IPv6/TrafficClass octet). Only ECN-Capable IP packets may be marked-those with the ECN field value of ECT(1) or ECT(0)  (binary 01 or 10, respectively). Not ECN-Capable Transport packets (ECN=00) never get marked. If a packet already has the CE mark (ECN=11), it never gets cleared, even if the device does not experience congestion.

Set ecn=yes on Tx Manager Queue to enable ECN marking.

ECN marking mechanism requires the respective Tx queues to use shared buffers (use-shared-buffers=yes).

The packet receives the CE mark if all conditions below are met:

1. The packet is either IPv4 or IPv6.
2. The ECN field value in IP header is either ECT(1) or ECT(0).
3. Egress port's Tx Queue has ecn=yes and uses shared buffers (use-shared-buffers=yes).
4. queueX-packet-use > queueX-shared-packet-cap or queueX-byte-use > queueX-shared-byte-cap. Since enabling ECN (ecn=yes) prevents ECN-capable packet drop, queue usage may exceed WRED thresholds if the traffic sender doesn't react to congestion notification in time.
### Priority-based Flow Control (PFC)

Priority-Based Flow Control (PFC) provides lossless operation for up to eight traffic classes, so that congestion in one traffic class does not pause other traffic classes. In addition, PFC enables co-existence of loss-sensitive traffic types with loss tolerant traffic type in the same network.

PFC-capable switch chips are complaint with IEEE 802.1Qbb PFC, meaning that the respective devices are capable of generating and responding to PFC frames. On the triggering part, the PFC frame is sent by the source port and traffic class experiencing the congestion. The timer values of the generated PFC frames are 0xFFFF for pause (XOFF) and 0x0 for resume (XON), and the appropriate bit in the priority enable vector is set. On the response part, the received PFC frame pauses the specific priority queues on the port that received the PFC frame for the duration specified by the PFC frame.

In RouterOS, PFC configuration is organized in profiles, where each port can be assigned to a specific profile. A PFC profile defines the traffic classes to enable PFC on, pause/resume thresholds to send XOFF/XON PFC frames, respectively, and whenever the assigned ports should transmit or/and receive PFC frames.

While congestion occurs on egress ports, PFC is triggered on the ingress port. Shared buffers must be used to associate the amount of ingressed traffic with the respective packets waiting in Tx queues. For each PFC-enabled traffic class, set use-shared-buffers=yes to the respective Tx Queues.

RouterOS implements 1:1 mapping between traffic classes and Tx queues. Packets with assigned traffic class 0 get enqueued in queue0, TC1 - queue1, etc., up to TC7-Q7. Hence, the terms "traffic class" and "tx queue" are used interchangeably in this text.

||during the delta time, lowering the overall throughput.|When choosing pause and resume thresholds, consider a delay in transmitting a PFC frame and processing it by the other side. For example, device A experienced congestion at time T, transmitted a PFC pause frame to device B, and B processed the frame and halted transmission at time T+D. During the delta time D, device B still kept sending traffic. If device A has configured the pause threshold to 100%, it has no free buffers available, and, therefore, packets may drop, which is unacceptable for lossless traffic classes. Lowering the pause threshold, let's say, down to 80% issues a PFC pause frame while still having free memory to accumulate traffic during the delta time D. The same applies to resume threshold. Setting it to 0% keeps the device idle PFC Rx requires setting the egress rate to all associated queues to calculate pause time, even if it matches the wire speed. For example, if PFC runs on traffic class 3, the assigned ports require the egress-rate-queue3 setting. /interface/ethernet/switch/qos/priority-flow-control add name=pfctc3 traffic-class=3 rx=yes /interface/ethernet/switch/qos/port set sfp-sfpplus1,sfp-sfpplus2 pfc=pfctc3 egress-rate-queue3=10G|
|---|---|---|
|Sub-menu:|Property Reference Switch settings Switch QoS settings (in addition to the existing ones).|/interface/ethernet/switch|
||Property|Description|
|Sub-menu:|qos-hw-offloading (yes | no; Default: no) reboot the device after disabling it. Port settings considered trusted.|Allows enabling QoS for the given switch chip (if the latter supports QoS). New generation devices force qos-hw-offloading=yes at all times. When you enable QoS, turning off the qos-hw-offloading setting will not completely revert to the previous functionality. It is recommended to /interface/ethernet/switch/qos/port Switch port QoS settings. Assigns a QoS profile to ingress packets on the given port. The assigned profile can be changed via match rules if the port is By default, ports are untrusted and receive the default QoS profile (Best-Effort, PCP=0, DSCP=0), where priority fields are cleared from the egress packets.|
||Property egress-rate-queue0 .. egress-rate-queue7 (integer: 0..18446744073709551615; Default !egress-rate-queuex) map (name; Default: default) pfc (name; Default: disabled) profile (name; Default: default)|Description Sets egress traffic limitation (bits per second) for specific output queue. It is possible to specify the limit using suffixes like k, M, or G to represent kbps, Mbps, or Gbps. This setting can be combined with the overall per-port limit egress-rate (see /in/eth/sw/port). Allows user-defined QoS priority-to-profile mapping in the case of a trusted port or host (see /in/eth/sw /qos/map). The name of the PFC profile to control ingress priority-based traffic flow (see /in/eth/sw/qos /priority-flow-control). The name of the QoS profile to assign to the ingress packets by default (see /in/eth/sw/qos/profile).|

trust-l2 (ignore | trust | keep; Default: ignore Whenever to trust the Layer 2 headers of the incoming packets (802.1p PCP field): ) ignore-ignore L2 header; use the port's profile value for all incoming packets; trust-use PCP field of VLAN-tagged packets for QoS profile lookup in map. Untagged packets use the port's profile value. Forwarded VLAN or priority-tagged packets receive the PCP value from the selected QoS profile (overwriting the original value). keep-trust but keep the original PCP value in forwarded packets.

trust-l3 (ignore | trust | keep; Default: ignore Whenever to trust the Layer 3 headers of the incoming packets (IP DSCP field): ) ignore-ignore L3 header; use either L2 header or the port's profile (depends on trust-l2). trust-use DSCP field of IP packets for QoS profile lookup in map. Forwarded/routed IP packets receive the DSCP value from the selected QoS profile (overwriting the original value). keep-trust but keep the original DSCP value in forwarded/routed packets.

tx-manager (name; Default: default) The name of the Transmission Manager that is responsible for enqueuing and transmitting packets from the given port (see**/in/eth/sw/qos/tx-manager**).

L3 trust mode has higher precedence than L2 unless trust-l3=ignore or the packet does not have an IP header.

Forwarded/routed packets obtain priority field values (PCP, DSCP) from the selected QoS profile, overwriting the original values unless the respective trust mode is set to keep.

Commands.

Command Description

print Print the above properties in a human-friendly format.

print stats Print port statistics: total and per-queue transmitted/dropped packets/bytes.

reset-counters Reset all counters in port statistics to zero.

print usage Print queue usage/resources.

print pfc Pring Priority Flow Control stats

print rates Print per-queue egress traffic limitation (set by egress-rate-queueX)

Port Stats

Example

[admin@Mikrotik] /interface/ethernet/switch/qos/port> print stats where name=ether2 name: ether2 tx-packet: 2 887 tx-byte: 3 938 897 drop-packet: 1 799 drop-byte: 2 526 144 tx-queue0-packet: 50 tx-queue1-packet: 1 871 tx-queue3-packet: 774 tx-queue5-packet: 192 tx-queue0-byte: 3 924 tx-queue1-byte: 2 468 585 tx-queue3-byte: 1 174 932 tx-queue5-byte: 291 456 drop-queue1-packet: 1 799 drop-queue1-byte: 2 526 144

Property Description

name Port name.

tx-packet The total number of packets transmitted via this port.

tx-byte The total number of bytes transmitted via this port.

drop-packet The total number of packets should have been transmitted via this port but were dropped due to a lack of resources (e.

g., queue buffers) or QoS Enforcement.
drop-byte The total number of bytes should have been transmitted via this port but were dropped.

tx-queue0-packet .. tx-queue7-The number of packets transmitted via this port from the respective queue. packet

tx-queue0-byte .. tx-queue7-The number of bytes transmitted via this port from the respective queue. byte

drop-queue0-packet .. drop-The number of packets dropped from the respective queue (or not enqueued at all due to lack of resources). queue7-packet

drop-queue0-byte .. drop-The number of bytes dropped from the respective queue. queue7-byte

Port Resources/Usage

Due to hardware limitations, some switch chip models may break traffic flow while accessing QoS port usage data. Use port usage for diagnostics/troubleshooting only. For monitoring, use QoS monitor or Port stats instead.

Example

[admin@crs326] /interface/ethernet/switch/qos/port> print usage where name=ether2 name: ether2 packet-cap: 136 packet-use: 5 byte-cap: 35 840 byte-use: 9 472 queue0-packet-cap: 130 queue0-packet-use: 1 queue1-packet-cap: 5 queue1-packet-use: 4 queue3-packet-cap: 65 queue3-packet-use: 2 queue0-byte-cap: 24 576 queue0-byte-use: 256 queue1-byte-cap: 7 680 queue1-byte-use: 6 144 queue3-byte-cap: 14 080 queue3-byte-use: 3 072

Property Description

name Port name.

packet-cap Port's packet capacity. The maximum number of packets that can be enqueued for transmission via the port.

packet-use 1 Port's packet usage. The number of packets that are currently enqueued in all port's queues.

byte-cap Port's byte capacity (buffer size). The maximum number of bytes that can be enqueued for transmission via the port.

byte-use 1 Port's byte usage. The size of hardware buffers (in bytes) that are currently allocated for packets the enqueued packets. Since the buffers are allocated by blocks (usually - 256B each), the allocated buffer size can be bigger than the actual payload.

queue0-packet-cap .. Individual queue capacity. The maximum number of packets that can be enqueued in the respective queues (unless the S queue7-packet-cap 2 hared Buffers are enabled).

queue0-shared-packet-cap Shared queue capacity (individual queue capacity + shared buffers). The maximum number of packets that can be .. queue7-shared-packet-enqueued in the respective queues. cap 2

queue0-packet-use .. Queue packet usage. The number of enqueued packets in the respective queues. queue7-packet-use 2

queue0-byte-cap .. queue7-Individual queue capacity. The maximum number of bytes that can be enqueued in the respective queues (unless the Shar byte-cap 2 ed Buffers are enabled).

queue0-shared-byte-cap .. Shared queue capacity (individual queue capacity + shared buffers). The maximum number of bytes that can be queue7-shared-byte-cap 2 enqueued in the respective queues.

queue0-byte-use .. queue7-Queue buffer usage (in bytes). The size of hardware buffers (in bytes) that are currently allocated for packets in the byte-use 2 respective queues.

queue0-byte-max .. Maximum queue buffer fill level (in bytes). Available only on devices that provide the queue statistics service. Use the reset queue7-byte-max 2-counters command to reset values.

1 Port's packet/byte usage can exceed the capacity if Shared Buffers are enabled. 2 Only the queues in use are printed.

Port PFC Stats (Previous Generations)

Example

[admin@crs317] /interface/ethernet/switch/qos/port> print pfc interval=1 where running name: sfp-sfpplus1 sfp-sfpplus2 ether1 pfc: roce disabled disabled pfc-tx: 46 pfc-paused-tc: 3 pfc3-pause-threshold: 1 048 576 pfc3-resume-threshold: 10 240 pfc3-use: 1 075 200

Property Description

name Port name.

pfc PFC profile name.

pfc-rx Received PFC frame count.

pfc-tx Transmitted PFC frame count.

pfc-paused-tc The list of traffic classes should be paused (from the sender's perspective). PFC pause frames (XOFF) are periodically sent with the listed timers set from this port.

pfc0-pause-threshold .. Pause thresholds of the respective traffic classes. Only PFC-enabled traffic classes are displayed. pfc7-pause-threshold

pfc0-resume-threshold .. Resume thresholds of the respective traffic classes. Only PFC-enabled traffic classes are displayed. pfc7-resume-threshold

pfc0-use .. pfc7-use The current buffer usage of the respective traffic classes (in bytes). In other words, it is the total size of all queued packets on all ports that were received from this port. Only PFC-enabled traffic classes are displayed.

Port PFC Stats (New Generations)

Example

[admin@crs812] /interface/ethernet/switch/qos/port> print pfc interval=1 where pfc=roce name: sfp56-5 pfc: roce rx-pause: 287 tx-pause: 46 pfc3-use: 2 184 200

Property Description

name Port name.

pfc PFC profile name.

pfc0-use .. The current buffer usage of the respective traffic classes (in bytes). In other words, it is the total size of all queued packets on all ports that pfc7-use were received from this port. Only PFC-enabled traffic classes are displayed.

rx-pause Received pause frame count.

tx-pause Transmitted pause frame count.

### QoS Menu

Sub-menu: /interface/ethernet/switch/qos

Almost the entire QoS HW configuration is located under **/in/eth/sw/qos**. Such an approach allows storing all QoS-related configuration items in one place, easy monitoring and exporting (/in/eth/sw/qos/export).

QoS entries have two major flags:

H-Hardware-offloaded. I-Inactive.

### QoS Settings

Sub-menu: /interface/ethernet/switch/qos/settings

Property Description

mirror-buffers ( Maximum amount of packet buffers for mirrored traffic (% of the total buffer memory). percent: 1..90; Default: auto)

mirror-profile ( The name of the QoS profile to assign to the mirrored packets (see **/in/eth/sw/qos/profile**). name; Default: default )

multicast-Maximum amount of packet buffers for multicast/broadcast traffic (% of the total buffer memory). buffers (perce nt: 1..90; Default: auto)

shared-Maximum amount of packet buffers that are shared between ports (% of the total buffer memory). Setting it to 0 disables buffer sharing. buffers (perce The remaining buffer memory is split between the ports. nt: 0..90; Default: auto) All buffers are treated as shared on new generation switch chips that use Dynamic Buffers. The switch chip automatically adjusts port and queue buffer limits based on the current congestion level. Using the auto value allows the device to utilize 100% of the available buffer memory, which is the recommended setting for most scenarios. In specific use cases where latency is more important than avoiding packet drops, the buffer limit can be manually reduced.

lossless-If the device supports multiple shared buffer pools, this setting allows adjusting the size of the lossless pool (% of the shared buffer buffers (perce memory, where 100% means all shared buffers allocated by the shared-buffers setting). For example, if shared-buffers=50 and nt: 0..100; lossless-buffers=80, the lossless pool receives 40% of the total buffer memory (80% of 50% or "0.8 * 0.5 = 0.4"), and the lossy pool Default: auto) receives the remaining 10% of shared buffers.

lossless-The list of lossless traffic classes. traffic-class (in teger array:

0..7; Default: auto) wred-A relative amount of packets above a shared queue cap ("queueX-shared-packet-cap" or "queueX-shared-byte-cap") where threshold (low random drops take place. This threshold is applied only to queues with enabled Weighed Random Early Detection (wred=yes) that use | medium | shared buffers (use-shared-buffers=yes). The higher the queue buffer fill level, the higher the packet drop chance. The low threshold high; Default: means the random tail drop starts later; the high-sooner. medium)
### QoS Monitor

Command: /interface/ethernet/switch/qos/monitor

Example

[admin@crs312] /interface/ethernet/switch/qos> monitor once total-packet-cap: 11 480 total-packet-use: 0 total-byte-cap: 2648.0KiB total-byte-use: 0 multicast-packet-cap: 1 148 multicast-packet-use: 0 multicast-byte-cap: 264.8KiB multicast-byte-use: 0 mirror-ingress-packet-cap: 1 148 mirror-ingress-packet-use: 0 mirror-ingress-byte-cap: 264.8KiB mirror-ingress-byte-use: 0 mirror-egress-packet-cap: 1 148 mirror-egress-packet-use: 0 mirror-egress-byte-cap: 264.8KiB mirror-egress-byte-use: 0 lossy-pool-packet-cap: 2 301 lossy-pool-packet-use: 0 lossless-pool-packet-cap: 2 301 lossless-pool-packet-use: 0 lossy-pool-byte-cap: 530.0KiB lossy-pool-byte-use: 0 lossless-pool-byte-cap: 530.0KiB lossless-pool-byte-use: 0

Monitors hardware QoS resources.

Property Description

total-Total packet capacity. The maximum number of hardware packet descriptors that the device can store is all queues. packet- cap (integ er)

total-Total packet usage. The current number of packet descriptors residing in the hardware memory. packet- use (integ er)

total-byte- cap (byte)

total-byte- use (byte)

multicast- packet- cap (integ er)

multicast- packet- use (integ er)

mirror- ingress- packet- cap (integ er)

mirror- ingress- packet- use (integ er)

mirror- ingress- byte-cap ( byte)

mirror- ingress- byte-use ( byte)

mirror- egress- packet- cap (integ er)

mirror- egress- packet- use (integ er)

mirror- egress- byte-cap ( byte)

mirror- egress- byte-use ( byte)

shared- packet- cap (integ er)

Total tx memory capacity.

Total tx memory usage. The current number of bytes occupied by the packets in all tx queues.

Multicast packet capacity. The maximum number of hardware packet descriptors that can be used by multicast/broadcast traffic. Depends on the multicast-buffers setting.

Multicast packet usage. The hardware makes a copy of the packet descriptor for each multicast destination.

Ingress mirror packet capacity. The maximum number of hardware packet descriptors that can be used by ingress mirrored traffic. Depends on the mirror-buffers setting.

Ingress mirror packet usage.

Ingress mirror byte capacity. Depends on the mirror-buffers setting.

Ingress mirror byte usage.

Egress mirror packet capacity. The maximum number of hardware packet descriptors that can be used by egress mirrored traffic. Depends on the mirror-buffers setting.

Egress mirror packet usage.

Egress mirror byte capacity. Depends on the mirror-buffers setting.

Egress mirror byte usage.

Shared packet capacity. The maximum number of hardware packet descriptors that can be shared between ports and tx queues. Depends on the shared-buffers setting.

shared- packet- use (integ er)

shared- byte-cap ( byte)

shared- byte-use ( byte)

lossy-pool- packet- cap (integ er)

lossy-pool- packet- use (integer)

lossless- pool- packet- cap (integer)

lossless- pool- packet- use (integer)

wred- packet- cap (integ er)

wred-byte- cap (integ er)

Shared packet usage. The current number of shared packet descriptors used by all tx queues.

Shared tx memory capacity. Depends on the shared-buffers setting.

Shared tx memory usage. The current number of shared buffers occupied by the packets in all tx queues.

Shared packet capacity of the lossy pool. The field is omitted if the device does not support multiple shared pools.

Shared packet usage of the lossy pool. The field is omitted if the device does not support multiple shared pools.

Shared packet capacity of the lossless pool. The field is omitted if the device does not support multiple shared pools.

Shared packet usage of the lossless pool. The field is omitted if the device does not support multiple shared pools.

The maximum packet count that a queue can use above the shared cap ("queueX-shared-packet-cap" in "/in/eth/sw/qos/port print usage") to trigger a random tail drop. For example, if "queue1-shared-packet-cap=3072" and "wred-packet-cap=512", WRED triggers when queue1-packet-use exceeds 3072, reaching 100% drop rate at 3072+512=3584 packets.

The maximum byte count that a queue can use above the shared cap ("queueX-shared-byte-cap") to trigger a random tail drop. For example, if "queue1-shared-byte-cap=768KiB" and "wred-byte-cap=128KiB", WRED triggers when queue1-packet-use excee ds 768KiB, reaching 100% drop rate at 768+128=896KiB.

Description

Traffic color for color-aware drop precedence management. Leave the default value (green) for color-blind drop precedence management.

IPv4/IPv6 DSCP field value for the egress packets assigned to the QoS profile.

The user-defined name of the QoS profile.

### QoS Profile

Sub-menu:

Property

color (green | yellow | red; Default: green )

dscp (integer : 0..63; Default:  )0

name (string; Default: )

/interface/ethernet/switch/qos/profile

QoS profiles determine priority field values (PCP, DSCP) for the forwarded/routed packets. Congestion avoidance/resolution is based on QoS profiles. Each packet gets a QoS profile assigned based on the ingress switch port QoS settings (see /in/eth/sw/port).

pcp (integer: VLAN priority value (IEEE 802.1q PCP-Priority Code Point). Used only if the egress packets assigned to the QoS profile are VLAN-

0..7; tagged (have the 802.1q header). The value can be further altered via the QoS Egress Map. Default:  )0 traffic-class (i The traffic class determines the packet priority and the egress queue (see tx-manager). The queue number is usually the same as the nteger: 0..7; traffic class (packets with tc0 go into queue0, tc1 - queue1, ... tc7 - queue7). Unlike pcp, where 0 means the default priority but 1 - the Default:  )0 lowest one (and further customizable), traffic classes are strictly ordered. TC0 always selects the lowest priority, etc. automap (yes Automatically map packets with matching PCP or DSCP values to this QoS profile. Only applies to trusted ports. | no; Default: yes)
### QoS Mapping

Sub-menu: /interface/ethernet/switch/qos/map

Priority-to-profile mapping table(-s) for trusted packets. All switch chips have one built-in map-default. In addition, some models allow the user to define custom mapping tables and assign different maps to various switch ports via the qos-map property:

devices based on Marvell Prestera 98DX224S, 98DX226S, or 98DX3236 switch chip models support only one map-default. devices based on Marvell Prestera 98DX8xxx, 98DX4xxx switch chips, or 98DX325x model devices support up to 12 maps (the default + 11 user- defined).

||defined).||
|---|---|---|
|Property||Description|
|name (string; Default: )||The user-defined name of the mapping table.|
|VLAN Map|||
|Sub-menu:|/interface/ethernet/switch/qos/map/vlan||
|Matches VLAN priorities (802.1p PCP/DEI fields) to QoS profiles. By default, all values are matched to the default QoS profile.|||
|Property||Description|
|dei-only (yes | no; Default: no)||Map only packets with DEI (formerly CFI) bit set in the VLAN header.|
|map (name; Default: default)||The name of the mapping table.|
|profile (name; Default: )||The name of the QoS profile to assign to the matched packets.|
|pcp (range: 0..7; Default:  )||0 VLAN priority (PCP) value(-s) for the lookup.|
|DSCP Map|||
|Sub-menu:|/interface/ethernet/switch/qos/map/ip||
|Matches DSCP values to QoS profiles.|||
|Property||Description|
|dscp (range: 0..63; Default:  )||0 DSCP value(-s) for the lookup.|
|map (name; Default: default)||The name of the mapping table. If not set, the standard (built-in) mapping table gets altered.|
|profile (name; Default: )||The name of the QoS profile to assign to the matched packets.|

### Transmission Manager

Sub-menu: /interface/ethernet/switch/qos/tx-manager

Transmission (Tx) Manager controls packet enqueuing for transmission and packet tx order. Different switch ports can be assigned to different Tx managers. The maximum number of hardware Tx managers depends on the switch chip model.

Property Description

name (string; The user-defined name of the Tx Manager Default: )

queue-buffers (perc The total amount of hardware Tx buffers allocated to all ports linked to this Tx Manager. Any value but auto is NOT scaled by the ent: 0%..100% | number of ports. For example, if queue-buffers=30%, and there are 3 ports using this Tx Manager, each respective port receives bytes | auto; Default: 10% of total available resources. Adding two more ports to the Tx Manager drops per-port buffers down to 6% (30/5). auto)

Port status has not effect on the allocated resources. Running ports receive the same amount of queue buffers as disconnected or disabled ones if all of them are assigned to the same Tx Manager.

Transmission Queue Scheduler

Sub-menu: /interface/ethernet/switch/qos/tx-manager/queue

Each port has eight Tx queues. The assigned Tx Manager controls packet enqueuing and schedules transmission orders. Each queue can have either strict priority (where packets with the highest traffic class are always transmitted first) or grouped together for a weighted round-robin tx schedule.

Creating a Tx Manager automatically creates all eight respective queue schedulers.

Changing any properties of Tx manager or queues completely halts traffic enqueueing and transmission during the offload process. Temporary packet loss is expected while the device is forwarding traffic.

Property Description

tx-manager (na The linked Tx Manager me read-only; )

traffic-class (int The traffic class (tc0..tc7) and the respective port queue (queue0..queue7) that the scheduler controls. eger: 0..7; read-only)

schedule (strict- priority | high- strict-priority-packets in the respective queue are always scheduled before moving to lower traffic classes. Packets with lower priority-group | traffic classes are not transmitted until the current queue is empty. low-priority-high-priority-group-all queues in the group are scheduled together by using a weighted round-robin principle. For example, if group ) TC5 has weight 4, TC4 - 3, and TC3 - 2, then the scheduler transmits 4 packets from queue5, 3 packets from Q4, and 2 packets from Q3 in a single round. To achieve lower latency, each round is "sliced" between all queues in the group. In other words, the packet order in each round of the above example is "Q5, Q4, Q3, Q5, Q4, Q3, Q5, Q4, Q5". low-priority-group-similar logic to the high-priority-group, but the low-priority-group is scheduled only when all queues in the high-priority-group are empty.

weight (integer: The weight value for the traffic class if it is a member of a schedule group. The field is not used in the case of strict priority schedule.

0..255; Default: 1 ) queue-buffers ( The amount of hardware Tx buffers allocated to this queue. Any value but auto is NOT scaled by the number of ports, i.e., the value percent: 0%.. gets split on ports linked to the Tx Manager. When given in percent, it means percentage of the tx-manager's queue-buffers value. 100% | bytes | auto; Default: a uto) use-shared-Allow the queue to use the shared buffer pool when queue-buffers are full. If the queue is full and the shared buffers are disabled, the buffers (yes | packet gets dropped. If the shared buffers are enabled, the queue may use up to shared-packet-cap or shared-poolX-packet-cap (see no) QoS Settings) packets from the shared pool. for details wred (yes | no; Enables/disables Weighted Random Early Detection for the given queue. Default: no)

ecn (yes | no; Enables/disables ECN marking of the transmitted packets. Default: no)

wred-actual (ye The actual WRED value. s | no;  read- only)

ecn-actual (yes The actual ECN value. | no;  read-only)

On some device models, due to hardware limitations, enabling ECN on one queue turns on CE marking of ECN-capable packets on all queues. In such cases, ecn-actual=yes despite ecn=no.

### Priority-based Flow Control (PFC)

Sub-menu: /interface/ethernet/switch/qos/priority-flow-control

PFC configuration is organized in profiles. Different switch ports can be assigned to different PFC profiles. The maximum number of hardware Tx managers depends on the switch chip model. The builtin profile named "disabled" cannot be changed.

Property Description

name (string; Default: ) The user-defined name of the PFC profile

pause-threshold (percent: Transmits a pause frame (XOFF) when the total size of enqueued packets reaches this threshold. Enqueued packets are 0%..100% | bytes | auto; counted per ingress port. Applies only when tx=yes. The value can be given either explicitly in bytes or percent of the Default: auto) respective shared pool size (shared-poolX-byte-cap).

resume-threshold (percen Transmits a resume frame (XON) when the total size of enqueued packets drops down to this threshold. Enqueued packets t: 0%..100% | bytes | auto; are counted per ingress port. Applies only when tx=yes. The value can be given either explicitly in bytes or percent of the Default: auto) respective shared pool size (shared-poolX-byte-cap).

rx (yes | no; Default: no) Enables receiving of PFC frames. The received PFC frame pauses the specific priority queues on the port that received the PFC frame for the duration specified by the PFC frame. Disabling rx disables queue pausing.

traffic-class (integer The list of PFC-enabled traffic classes. array: 0..7)

tx (yes | no; Default: no) Enables transmition of PFC frames.

||Introduction Features Setup Examples See also Introduction|Switch Chip Features Port Switching Port Mirroring Port Settings VLAN Table Host Table Rule Table Port isolation Private VLAN CPU Flow Control Statistics Management access configuration Tagged Untagged Inter-VLAN routing "Port Switching" feature, but there are a few with more features:|Switch All Ports Feature Isolated switch groups VLAN Example 1 (Trunk and Access Ports) VLAN Example 2 (Trunk and Hybrid Ports) Untagged from tagged port||There are several types of switch chips on Routerboards and they have different sets of features. Most of them (from now on "Other") have only the basic||||||||
|---|---|---|---|---|---|---|---|---|---|---|---|---|
|Feature|QCA8337|Atheros8327|Atheros8316|Atheros8227|Atheros7240|IPQ- PPE|ICPlus175D|MT7621, MT7531|EN7523|RTL8367|88E6393X|88E6191X, 88E6190|
|Port Switching Port Mirroring TX limit 1 RX limit 1 Host table Vlan table Rule table Notes|yes yes yes yes 2048 entries 4096 entries 92 rules menu.|yes yes yes yes 2048 entries 4096 entries 92 rules configuration is not supported.|yes yes yes no 2048 entries 4096 entries 32 rules|yes yes yes no 1024 entries 4096 entries no 3. Bridge HW vlan-filtering was added in the RouterOS 7.1 for RTL8367, MT7621, MT7531, EN7523. Marvell Prestera switch (e.g. CRS3xx), see Marvell Prestera switch chip features manual.|yes yes yes no 2048 entries 16 entries no 2. MAC addresses are learned up to the specified number, but the content of a switch host table is not available in RouterOS and static host type 0x88a8 or 0x9100 (only 0x8100 is supported) and no tag-stacking. Using these features will disable HW offload.|yes no no no 2048 entries no no 1. For QCA8337, Atheros8327, Atheros8316, Atheros8227, and Atheros7240 the Tx/Rx rate limits can be changed with bandwidth property on "/i nterface ethernet" menu, see more details in the Ethernet manual. For RTL8367, 88E6393X, 88E6191X, 88E6190, MT7621, MT7531 and EN7523 Tx/Rx rate limit can be changed with egress-rate and ingress-rate properties on "/interface ethernet switch port" Cloud Router Switch (CRS) series devices have highly advanced switch chips built-in, they support a wide variety of features. For more details about switch chip capabilities on CRS1xx/CRS2xx series devices check the CRS1xx/CRS2xx series switches manual, for MikroTik devices with|yes yes no no 2048 entries 2 no no|yes yes yes yes 2048 entries 4096 entries 3 no|yes yes yes yes 1024 entries 4096 entries 3 no|yes yes yes yes 2048 entries 4096 entries 3 no|yes yes yes yes 16k entries 4096 entries 3 256 otherThe switch does not support|yes yes yes yes 16k entries 4096 entries 3 no ether-|

RouterBoard

cAPGi-5HaxD2HaxD (cAP ax)

L009 series

RB5009 series

CCR2004-16G-2S+

RB4011iGS+

RB1100AHx4

L41G-2axD (hAP ax lite)

RB750Gr3 (hEX), RB760iGS (hEX S)

E50UG (hEX Refresh)

RBM33G

RB3011 series

RB OmniTik ac series

RBwsAP-5Hac2nD (wsAP ac lite)

RB941-2nD (hAP lite)

RB953GS

RB850Gx2

RB2011 series

LTE12)

(Audience LTE6 kit),

RBD22UGS-5HPacD2HnD (mANTBox 52 15s)

RB1100AH

RB1100AHx2

CCR1009-8G-1S-1S+; CCR1009-8G-1S

Switch-chip description

IPQ-PPE (ether1-ether2)

88E6190 (ether2-ether8, sfp1)

88E6393X (ether1-ether8, sfp- sfpplus1)

88E6191X (ether1-ether8); 88E6191X (ether9-ether16);

RTL8367 (ether1-ether5); RTL8367 (ether6-ether10);

RTL8367 (ether1-ether5); RTL8367 (ether6-ether10); RTL8367 (ether11- ether13)

MT7531 (ether1-ether4)

MT7621 (ether1-ether5)

EN7523 (ether2-ether5)

MT7621 (ether1-ether3)

QCA8337 (ether1-ether5); QCA8337 (ether6-ether10)

QCA8337 (ether1-ether5)

Atheros8227 (ether1-ether3)

Atheros8227 (ether1-ether4)

Atheros8327 (ether1-ether3+sfp1)

Atheros8327 (ether1-ether5) with ether1 optional

Atheros8327 (ether1-ether5+sfp1); Atheros8227 (ether6-ether10)

Atheros8327 (ether1-sfp1)

Atheros8327 (ether1-ether5); Atheros8327 (ether6-ether10)

Atheros8327 (ether1-ether5); Atheros8327 (ether6-ether10)

Atheros8327 (ether1-ether4)

C52iG-5HaxD2HaxD-TC (hAP ax2), C53UiG+5HPaxD2HPaxD (hAP ax3), Chateau ax series IPQ-PPE (ether1-ether5)

RB951Ui-2nD (hAP); RB952Ui-5ac2nD (hAP ac lite); RB750r2 (hEX lite); RB750UPr2 (hEX PoE lite); RB750P-Atheros8227 (ether1-ether5) PBr2 (PowerBox); RB750P r2; RBOmniTikU-5HnDr2 (OmniTIK 5); RBOmniTikUPA-5HnDr2 (OmniTIK 5 PoE)

RB750Gr2 (hEX); RB962UiGS-5HacT2HnT (hAP ac); RB960PGS (hEX PoE); RB960PGS-PB (PowerBox Pro) QCA8337 (ether1-ether5)

RB750GL; RB751G-2HnD; RB951G-2HnD; RBD52G-5HacD2HnD (hAP ac²), RBD53iG-5HacD2HnD (hAP Atheros8327 (ether1-ether5) ac³), RBD53GR-5HacD2HnD&R11e-LTE6 (hAP ac³ LTE6 kit), RBD53G-5HacD2HnD-TC&EG12-EA (Chateau

RBcAPGi-5acD2nD (cAP ac), RBwAPGR-5HacD2HnD (wAP R ac and wAP ac LTE series), RBwAPG-Atheros8327 (ether1-ether2) 5HacD2HnD (wAP ac), RBD25G-5HPacQD2HPnD (Audience), RBD25GR-5HPacQD2HPnD&R11e-LTE6

|RB493G|Atheros8316 (ether1+ether6-ether9);|
|---|---|
||Atheros8316 (ether2-ether5)|
|RB435G|Atheros8316 (ether1-ether3) with ether1 optional|
|RB450G|Atheros8316 (ether1-ether5) with ether1 optional|
|RB450Gx4|Atheros8327 (ether1-ether5)|
|RB433GL|Atheros8327 (ether1-ether3)|
|RB750G|Atheros8316 (ether1-ether5)|
|RB1200|Atheros8316 (ether1-ether5)|
|RB1100|Atheros8316 (ether1-ether5); Atheros8316 (ether6-ether10)|
|DISC Lite5|Atheros8227 (ether1)|
|RBmAP2nD|Atheros8227 (ether1-ether2)|
|RBmAP2n|Atheros7240 (ether1-ether2)|
|RB750|Atheros7240 (ether2-ether5)|
|RB750UP|Atheros7240 (ether2-ether5)|
|RB751U-2HnD|Atheros7240 (ether2-ether5)|
|RB951-2n|Atheros7240 (ether2-ether5)|
|RB951Ui-2HnD|Atheros8227 (ether1-ether5)|
|RB433 series|ICPlus175D (ether2-ether3); older models had ICPlus175C|
|RB450|ICPlus175D (ether2-ether5); older models had ICPlus175C|
|RB493 series|ICPlus178C (ether2-ether9)|
|RB816 The command-line configuration is under the switch menu. This menu contains a list of all switch chips present in the system and some sub-menus as well. [admin@MikroTik] > /interface ethernet switch print Flags: I-invalid # NAME TYPE MIRROR-SOURCE MIRROR-TARGET SWITCH-ALL-PORTS 0 switch1 Atheros-8327 none none 1 switch2 Atheros-8227 none none|ICPlus178C (ether1-ether16)|

Depending on the switch type there can be different configuration capabilities available.

## <u>Features</u>

### Port Switching

To set up port switching on non-CRS series devices, check the Bridge Hardware Offloading page.

Port switching in RouterOS v6.41 and newer is done using the bridge configuration. Before RouterOS v6.41 port switching was done using the m aster-port property.

Switch All Ports Feature

Ether1 port on RB450G/RB435G/RB850Gx2 devices has a feature that allows it to be removed/added to the default switch group, this setting is available on the /interface ethernet switch menu. By default ether1 port will be included in the switch group.

Property Description

switch-all-ports (no | Changes ether1 switch group only on RB450G/RB435G/RB850Gx2 devices. yes; Default: yes) yes - ether1 is part of the switch and supports switch grouping and all other advanced Atheros8316/Atheros8327 features including extended statistics (/interface ethernet print stats). no-ether1 is not part of the switch, effectively making it a stand-alone ethernet port, this way increasing its throughput to other ports in bridged and routed mode, but removing the switching possibility on this port.

### Port Mirroring

Port mirroring lets the switch to copy all traffic that is going in and out of one port (mirror-source) and send out these copied frames to some other port ( mirror-target). This feature can be used to easily set up a 'tap' device that receives all traffic that goes in/out of some specific port. Note that mirror- source and mirror-target ports have to belong to the same switch (see which port belongs to which switch in /interface ethernet menu). Also, mirror-target can have a special 'cpu' value, which means that mirrored packets should be sent out to the switch chips CPU port. Port mirroring happens independently of switching groups that have or have not been set up.

Sub-menu: /interface ethernet switch

Property Description

mirror-source (name | Selects a single mirroring source port. Ingress and egress traffic will be sent to the mirror-target port. Note that mirror- none; Default: none) target port has to belong to the same switch (see which port belongs to which switch in /interface ethernet menu).

mirror-target (name | Selects a single mirroring target port. Mirrored packets from mirror-source and mirror (see the property in rule and host none | cpu; Default: none table) will be sent to the selected port. )

mirror-egress-target (na Selects a single mirroring egress target port, only available on 88E6393X, 88E6191X and 88E6190 switch chips. Mirrored me | none; Default: none packets from mirror-egress (see the property in port menu) will be sent to the selected port. )

Sub-menu: /interface ethernet switch rule

Property Description

||mirror (no | yes; Default: no) mirror-ports (name; Default:)|Sub-menu: /interface ethernet switch host|Whether to send a packet copy to mirror-target port. Selects multiple mirroring target ports, only available on 88E6393X switch chip. Matched packets in the ACL rule will be copied and sent to selected ports.|
|---|---|---|---|
||Property||Description|
||mirror (no | yes; Default: no)|Sub-menu: /interface ethernet switch port|Whether to send a frame copy to mirror-target port from a frame with a matching MAC destination address (matching destination or source address for CRS3xx series switches)|
||Property||Description|
||mirror-egress (no | yes; Default: no) mirror-ingress (no | yes; Default: no) mirror-ingress-target (name | none; Default: none) inaccessible. Port Settings|Port mirroring configuration example: /interface ethernet switch|Whether to send egress packet copy to the mirror-egress-target port, only available on 88E6393X, 88E6191X and 88E6190 switch chips. Whether to send ingress packet copy to the mirror-ingress-target port, only available on 88E6393X, 88E6191X and 88E6190 switch chips. Selects a single mirroring ingress target port, only available on  88E6393X, 88E6191X and 88E6190 switch chips. Mirrored packets from mirror-ingress will be sent to the selected port. set switch1 mirror-source=ether2 mirror-target=ether3 If you set mirror-source as an Ethernet port for a device with at least two switch chips and these mirror-source ports are in a single bridge while mirror-target for both switch chips are set to send the packets to the CPU, then this will result in a loop, which can make your device Properties under this menu are used to configure VLAN switching and filtering options for switch chips that support a VLAN Table. These properties are only available to switch chips that have VLAN Table support, check the Switch Chip Features table to make sure your device supports such a feature. Ingress traffic is considered as traffic that is being sent IN a certain port, this port is sometimes called ingress port. Egress traffic is considered as traffic that is being sent OUT of a certain port, this port is sometimes called egress port. Distinguishing them is very important to properly set up VLAN filtering since some properties apply only to either ingress or egress traffic.|
||Property||Description|
|led)|vlan-mode (check | disabled | fallback | secure; Default: disab||Changes the VLAN lookup mechanism against the VLAN Table for ingress traffic. disabled-disables checking against the VLAN Table completely for ingress traffic. No traffic is dropped when set on the ingress port. fallback-checks tagged traffic against the VLAN Table for ingress traffic and forwards all untagged traffic. If ingress traffic is tagged and the egress port is not found in the VLAN table for the appropriate VLAN ID, then traffic is dropped. If a VLAN ID is not found in the VLAN Table, then traffic is forwarded. Used to allow known VLANs only in specific ports. check-checks tagged traffic against the VLAN Table for ingress traffic and drops all untagged traffic. If ingress traffic is tagged and the egress port is not found in the VLAN table for the appropriate VLAN ID, then traffic is dropped. secure-checks tagged traffic against the VLAN Table for ingress traffic and drops all untagged traffic. Both ingress and egress port must be found in the VLAN Table for the appropriate VLAN ID, otherwise, traffic is dropped.|

vlan-header (add-if-Sets action which is performed on the port for egress traffic. missing | always-strip | leave-as-is; Default: add-if-missing - adds a VLAN tag on egress traffic and uses default-vlan-id from the ingress port. Should be used for leave-as-is) trunk ports. always-strip-removes a VLAN tag on egress traffic. Should be used for access ports. leave-as-is-does not add nor remove a VLAN tag on egress traffic. Should be used for hybrid ports.

default-vlan-id (auto | Adds a VLAN tag with the specified VLAN ID on all untagged ingress traffic on a port, should be used with vlan-header set to al integer: 0..4095; ways-strip on a port to configure the port to be the access port. For hybrid ports default-vlan-id is used to tag untagged Default: auto) traffic. If two ports have the same default-vlan-id, then VLAN tag is not added since the switch chip assumes that traffic is being forwarded between access ports.

On QCA8337 and Atheros8327 switch chips, a default vlan-header=leave-as-is property should be used. The switch chip will determine which ports are access ports by using the default-vlan-id property. The default-vlan-id should only be used on access/hybrid ports to specify which VLAN the untagged ingress traffic is assigned to.

### VLAN Table

VLAN table specifies certain forwarding rules for packets that have a specific 802.1Q tag. Those rules are of higher priority than switch groups configured using the Bridge Hardware Offloading feature. Basically, the table contains entries that map specific VLAN tag IDs to a group of one or more ports. Packets with VLAN tags leave the switch chip through one or more ports that are set in the corresponding table entry. The exact logic that controls how packets with VLAN tags are treated is controlled by a vlan-mode parameter that is changeable per switch port.

VLAN ID based forwarding takes into account the MAC addresses dynamically learned or manually added in the host table. QCA8337 and Atheros8327 switch-chips also support Independent VLAN Learning (IVL) which does the learning based on both-MAC addresses and VLAN IDs, thus allowing the same MAC to be used in multiple VLANs.

Packets without VLAN tag are treated just as if they had a VLAN tag with port default-vlan-id. If vlan-mode=check or vlan=mode=secure is configured, to forward packets without VLAN tags you have to add an entry to the VLAN table with the same VLAN ID according to default-vlan-id.

Property Description

disabled (no | yes; Default: no) Enables or disables switch VLAN entry.

independent-learning (no | yes; Whether to use shared-VLAN-learning (SVL) or independent-VLAN-learning (IVL). Default: yes)

ports (name; Default: none) Interface member list for the respective VLAN. This setting accepts comma-separated values. e.g. ports=eth er1,ether2.

switch (name; Default: none) Name of the switch for which the respective VLAN entry is intended for.

vlan-id (integer: 0..4095; Default: ) The VLAN ID for certain switch port configurations.

Devices with MT7621, MT7531, EN7523, RTL8367, 88E6393X, 88E6191X, 88E6190 switch chips support HW offloaded vlan-filtering in RouterOS v7. VLAN-related configuration on the "/interface ethernet switch" menu is not available.

### VLAN Forwarding

Both vlan-mode and vlan-header along with the VLAN Table can be used to configure VLAN tagging, untagging and filtering, multiple combinations are possible, each achieving a different result. Below you can find a table of what kind of traffic is going to be sent out through an egress port when a certain traffic is received on an ingress port for each VLAN Mode.

NOTES:

L-vlan-header is set to leave-as-is S-vlan-header set to always-strip A-vlan-header set to add-if-missing U-Untagged traffic is sent out T-Tagged traffic is sent out, a tag is already present on the ingress port TA-Tagged traffic is sent out, a tag was added on the ingress port DI - Traffic is dropped on ingress port because of mode selected in vlan-mode

||DE-Traffic is dropped on egress port because egress port was not found in the VLAN Table VID match-VLAN ID from the VLAN tag for ingress traffic is present in the VLAN Table Port match-Ingress port is present in the VLAN Table for the appropriate VLAN ID||||||
|---|---|---|---|---|---|---|
|VLAN Mode = disabled||Egress port not present in VLAN Table|||Egress port is present in VLAN Table||
||L|S|A|L|S|A|
|Untagged traffic|U|U|TA|U|U|TA|
|Tagged traffic; no VID match|T|U|T||||
|Tagged traffic; VID match; no Port match|T|U|T|T|U|T|
|Tagged traffic; VID match; Port match|T|U|T|T|U|T|
|VLAN Mode = fallback||Egress port not present in VLAN Table|||Egress port is present in VLAN Table||
||L|S|A|L|S|A|
|Untagged traffic|U|U|TA|U|U|TA|
|Tagged traffic; no VID match|T|U|T||||
|Tagged traffic; VID match; no Port match|DE|DE|DE|T|U|T|
|Tagged traffic; VID match; Port match|DE|DE|DE|T|U|T|
|VLAN Mode = check||Egress port not present in VLAN Table|||Egress port is present in VLAN Table||
||L|S|A|L|S|A|
|Untagged traffic|||||||
|Tagged traffic; no VID match|DI|DI|DI||||
|Tagged traffic; VID match; no Port match|DE|DE|DE|T|U|T|
|Tagged traffic; VID match; Port match|DE|DE|DE|T|U|T|
|VLAN Mode = secure||Egress port not present in VLAN Table|||Egress port is present in VLAN Table||
||L|S|A|L|S|A|
|Untagged traffic|||||||
|Tagged traffic; no VID match|DI|DI|DI||||
|Tagged traffic; VID match; no Port match|DI|DI|DI|DI|DI|DI|
|Tagged traffic; VID match; Port match|DE|DE|DE|T|U|T|
|each VLAN related property. Host Table|||The tables above are meant for more advanced configurations and to double-check your understanding of how packets will be processed with||||

The host table represents switch chip's internal MAC address to port mapping. It can contain two kinds of entries: dynamic and static. Dynamic entries get added automatically, this is also called a learning process: when switch chip receives a packet from a certain port, it adds the packet's source MAC address and port it received the packet from to the host table, so when a packet comes in with the same destination MAC address, it knows to which port it should forward the packet. If the destination MAC address is not present in the host table (so-called unknown-unicast traffic) then it forwards the packet to all ports in the group. Dynamic entries take about 5 minutes to time out. Learning is enabled only on ports that are configured as part of the switch group, so you won't see dynamic entries if you have not set up port switching. Also, you can add static entries that take over dynamic if a dynamic entry with the same MAC address already exists. Since port switching is configured using a bridge with hardware offloading, any static entries created on one table (either bridge host or switch host) will appear on the opposite table as a dynamic entry. Adding a static entry on the switch host table will provide access to some more functionality that is controlled via the following params:

Property Description

copy-to-cpu (no | yes; Whether to send a frame copy to switch CPU port from a frame with a matching MAC destination address (matching Default: no) destination or source address for CRS3xx series switches)

drop (no | yes; Default: Whether to drop a frame with a matching MAC source address received on a certain port (matching destination or source no) address for CRS3xx series switches)

mac-address (MAC; Def Host's MAC address ault: 00:00:00:00:00:00)

mirror (no | yes; Default: Whether to send a frame copy to mirror-target port from a frame with a matching MAC destination address (matching no) destination or source address for CRS3xx series switches)

ports (name; Default: no Name of the interface, static MAC address can be mapped to more than one port, including switch CPU port ne)

redirect-to-cpu (no | yes Whether to redirect a frame to switch CPU port from a frame with a matching MAC destination address (matching destination; Default: no) or source address for CRS3xx series switches)

share-vlan-learned (no | Whether the static host MAC address lookup is used with shared-VLAN-learning (SVL) or independent-VLAN-learning (IVL). yes; Default: no) The SVL mode is used for those VLAN entries that do not support IVL or IVL is disabled (independent-learning=no)

switch (name; Default: n Name of the switch to which the MAC address is going to be assigned to one)

vlan-id (integer: 0..4095; VLAN ID for the statically added MAC address entry Default: )

Every switch chip has a finite number of MAC addresses it can store on the chip, see the Introduction table for a specific host table size. Once a host table is full, different techniques can be utilized to cope with the situation, for example, the switch can remove older entries to free space for more recent MAC addresses (used on QCA-8337 and Atheros-8327 switch chips), another option is to simply ignore the new MAC addresses and only remove entries after a timeout has passed (used on Atheros8316, Atheros8227, Atheros-7240, ICPlus175D and Realtek-RTL8367 switch chips), the last option is a combination of the previous two-only allow a certain amount of entries to be renewed and keep the other host portion intact till the timeout (used on MediaTek-MT7621, MT7531, EN7523 switch chip). These techniques cannot be changed with configuration.

For Atheros8316, Atheros8227 and Atheros-7240 switch chips, the switch-cpu port will always participate in the host learning process when at least one hardware offloaded bridge port is active on the switching group. It will cause the switch-cpu port to learn MAC addresses from non- HW offloaded interfaces. This might cause packet loss when a single bridge contains HW and non-HW offloaded interfaces. Also, packet loss might appear when a duplicate MAC address is used on the same switching group regardless if hosts are located on different logical networks. It is recommended to use HW offloading only when all bridge ports can use HW offloaded or keep it disabled on all switch ports when one or more bridge ports cannot be configured with HW offloading.

||Rule Table|entries, these MAC addresses are only assigned to VLAN 1. To ensure packets with these destination MAC addresses are processed correctly:|The switch chips QCA-8337 and Atheros-8327 automatically add reserved mulitcast MAC addresses (01:80:C2:00:00:0x) to the host table when hardware-offloaded bridge is created with forward-reserved-addresses=no and protocol-mode=stp/rstp. These MACs should not be forwarded by 802.1Q compatible bridges and they are essential for correct operation with R/STP. Since the switch has a limited number of host table Switch ports should be set to default VLAN 1 (default-vlan-id=auto or default-vlan-id=1). If VLAN 1 is explicitly configured, it must use independent VLAN learning (independent-learning=yes). Rule table is a very powerful tool allowing wire-speed packet filtering, forwarding and VLAN tagging based on L2, L3 and L4 protocol header field conditions. The menu contains an ordered list of rules just like in /ip firewall filter, so ACL rules are checked for each packet until a match has been found. If multiple rules can match, then only the first rule will be triggered. A rule without any action parameters is a rule to accept the packet. Each rule contains a conditions part and an action part. The action part is controlled by the following parameters:|
|---|---|---|---|
||Property|Description||
|)|copy-to-cpu (no | yes; Default: no) mirror (no | yes; Default: no) new-dst-ports (na me; Default: none) new-vlan-id (integ er: 0..4095) new-vlan-priority (integer: 0..7) rate (integer: 0.. 4294967295) redirect-to-cpu (n o | yes; Default: no|Whether to send a packet copy to switch CPU port Whether to send a packet copy to mirror-target port chips) applies to Atheros8327/QCA8337 switch chips) The conditions part is controlled by the rest of the parameters:|Changes the destination port as specified, multiple ports allowed, including a switch CPU port. An empty setting will drop the packet. When the parameter is not used, the packet will be accepted Changes the VLAN ID to the specified value or adds a new VLAN tag if one was not already present (the property only applies to the Atheros8316, and 88E6393X switch chips (NOTE: in case of 88E6393X switch chip, vlan-filtering=yes is also required) Changes the VLAN priority field (priority code point, the property only applies to Atheros8327, QCA8337 and Atheros8316 switch Sets ingress traffic limitation (bits per second) for matched traffic, can only be applied to the first 32 rule slots (the property only Changes the destination port of a matching packet to the switch CPU|
||Property dscp (integer: 0..63) dst-port (integer: 0..65535) 65535 | or 0x0000-0xffff)|disabled (no | yes; Default: no) dst-address (IP address/Mask) dst-address6 (IPv6 address/Mask) dst-mac-address (MAC address/Mask) flow-label (integer: 0..1048575) mac-protocol (802.2 | arp | capsman | dot1x | homeplug-av | ip | ipv6 | ipx | lacp | lldp | loop-protect | macsec | mpls-multicast | mpls-unicast | mvrp | packing-compr | packing-simple | pppoe | pppoe-discovery | rarp | romon | service-vlan | vlan | or 0..|Description Enables or disables switch rule Matching DSCP field of the packet Matching destination IP address and mask Matching destination IPv6 address and mask Matching destination MAC address and mask Matching destination protocol port number or range Matching IPv6 flow label Matching particular MAC protocol specified by protocol name or number (skips VLAN tags if any)|

ports (name)

protocol (dccp | ddp | egp | encap | etherip | ggp | gre | hmp | icmp | icmpv6 | idpr- cmtp | igmp | ipencap | ipip | ipsec-ah | ipsec-esp | ipv6 | ipv6-frag | ipv6-nonxt | ipv6- opts | ipv6-route | iso-tp4 | l2tp | ospf | pim | pup | rdp | rspf | rsvp | sctp | st | tcp | udp | udp-lite | vmtp | vrrp | xns-idp | xtp | or 0..255)

src-address (IP address/Mask)

src-address6 (IPv6 address/Mask)

src-mac-address (MAC address/Mask)

src-port (0..65535)

switch (switch group)

traffic-class (0..255)

vlan-id (0..4095)

vlan-header (not-present | present)

vlan-priority (0..7)

IPv4 and IPv6 specific conditions cannot be present in the same rule.

Name of the interface on which the rule will apply on the received traffic, multiple ports are allowed. If ports property is left empty, the rule will apply to all switch interfaces

Matching particular IP protocol specified by protocol name or number

Matching source IP address and mask

Matching source IPv6 address and mask

Matching source MAC address and mask

Matching source protocol port number or range

Matching switch group on which will the rule apply

Matching IPv6 traffic class

Matching VLAN ID (the property only applies to the Atheros8316, Atheros8327, QCA8337, 88E6393X switch chips)

Matching VLAN header, whether the VLAN header is present or not (the property only applies to the Atheros8316, Atheros8327, QCA8337, 88E6393X switch chips. in case of 88E6393X switch chip, vlan-filtering=yes is also required)

Matching VLAN priority (priority code point)

those rules did not fit into the switch chip.

### Port isolation

Switch port isolation is available on all switch chips since RouterOS v6.43.

Property Description

Default: ) them with a comma.

send packets through all switch ports.

Because the rule table is processed entirely in switch chips hardware, there is a limitation to how many rules you may have. Depending on the number of conditions (MAC layer, IP layer, IPv6, L4 layer) you use in your rules, the number of active rules may vary from 8 to 32 for Atheros8316 switch chip, from 8 to 16 for Atheros8327/QCA8337 switch chip and from 42 to 256 for 88E6393X switch chip. You can always do / interface ethernet switch rule print after modifying your rule set to see that no rules at the end of the list are 'invalid' which means

Port isolation provides the possibility to divide (isolate) certain parts of your network, this might be useful when you need to make sure that certain devices cannot access other devices, this can be done by isolating switch ports. Port isolation only works between ports that are members of the same switch.

forwarding-override (interface; Forces ingress traffic to be forwarded to a specific interface. Multiple interfaces can be specified by separating

(R/M)STP will only work properly in PVLAN setups, (R/M)STP will not work properly in setups, where there are multiple isolated switch groups, because switch groups might not properly receive BPDUs and therefore fail to detect network loops.

The forwarding-override property affects ingress traffic only. Switch ports that do not have the forwarding-override specified can

Switch chips with a VLAN table support (QCA8337, Atheros8327, Atheros8316, Atheros8227 and Atheros7240) can override the port isolation configuration when enabling a VLAN lookup on the switch port (the vlan-mode is set to fallback, check or secure). If additional port isolation is needed between ports on the same VLAN, a switch rule with a new-dst-ports property can be implemented. Other devices without switch rule support cannot overcome this limitation.

Private VLAN

In some scenarios, you might need to forward all traffic to an uplink port while all other ports are isolated from each other. This kind of setup is called Privat e VLAN configuration, the Switch will forward all Ethernet frames directly to the uplink port allowing the Router to filter unwanted packets and limit access between devices that are behind switch ports.

To configure switch port isolation, you need to switch all required ports:

/interface bridge add name=bridge1 /interface bridge port add interface=sfp1 bridge=bridge1 hw=yes add interface=ether1 bridge=bridge1 hw=yes add interface=ether2 bridge=bridge1 hw=yes add interface=ether3 bridge=bridge1 hw=yes

By default, the bridge interface is configured with protocol-mode set to rstp. For some devices, this can disable hardware offloading because specific switch chips do not support this feature. See the Bridge Hardware Offloading section with supported features.

Override the egress port for each switch port that needs to be isolated (excluding the uplink port):

/interface ethernet switch port-isolation set ether1 forwarding-override=sfp1 set ether2 forwarding-override=sfp1 set ether3 forwarding-override=sfp1

It is possible to set multiple uplink ports for a single switch chip, this can be done by specifying multiple interfaces and separating them with a comma.

Isolated switch groups

In some scenarios you might need to isolate a group of devices from other groups, this can be done using the switch port isolation feature. This is useful when you have multiple networks but you want to use a single switch, with port isolation you can allow certain switch ports to be able to communicate through only a set of switch ports. In this example, devices on ether1-3 will only be able to communicate with devices that are on ether1-3, while devices on ether4-5 will only be able to communicate with devices on ether4-5 (ether1-3 is not able to communicate with ether4-5)

Port isolation is only available between ports that are members of the same switch.

To configure isolated switch groups you must first switch all ports:

/interface bridge add name=bridge /interface bridge port add bridge=bridge1 interface=ether1 hw=yes add bridge=bridge1 interface=ether2 hw=yes add bridge=bridge1 interface=ether3 hw=yes add bridge=bridge1 interface=ether4 hw=yes add bridge=bridge1 interface=ether5 hw=yes

By default, the bridge interface is configured with protocol-mode set to rstp. For some devices, this can disable hardware offloading because specific switch chips do not support this feature. See the Bridge Hardware Offloading section with supported features.

Then specify in the forwarding-override property all ports that you want to be in the same isolated switch group (except the port on which you are applying the property), for example, to create an isolated switch group for A devices:

/interface ethernet switch port-isolation set ether1 forwarding-override=ether2,ether3 set ether2 forwarding-override=ether1,ether3 set ether3 forwarding-override=ether1,ether2

To create an isolated switch group for B devices:

/interface ethernet switch port-isolation set ether4 forwarding-override=ether5 set ether5 forwarding-override=ether4

### CPU Flow Control

All switch chips have a special port that is called switchX-cpu, this is the CPU port for a switch chip, it is meant to forward traffic from a switch chip to the CPU, such a port is required for management traffic and routing features. By default the switch chip ensures that this special CPU port is not congested and sends out Pause Frames when link capacity is exceeded to make sure the port is not oversaturated, this feature is called CPU Flow Control. Without this feature packets that might be crucial for routing or management purposes might get dropped.

Since RouterOS v6.43 it is possible to disable the CPU Flow Control feature on some devices that are using one of the following switch chips: QCA8337, Atheros8227, Atheros8327, Atheros7240, Atheros8316, 88E6191X and 88E6393X . Other switch chips have this feature enabled by default and cannot be changed. To disable CPU Flow Control use the following command:

/interface ethernet switch set switch1 cpu-flow-control=no

Statistics

Some switch chips are capable of reporting statistics, this can be useful to monitor how many packets are sent to the CPU from the built-in switch chip. These statistics can also be used to monitor CPU Flow Control. You can find an example of the switch chip's statistics below:

[admin@MikroTik] > /interface ethernet switch print stats

name: switch1 driver-rx-byte: 221 369 701 driver-rx-packet: 1 802 975 driver-tx-byte: 42 621 969 driver-tx-packet: 310 485 rx-bytes: 414 588 529 rx-packet: 2 851 236 rx-too-short: 0 rx-too-long: 0 rx-broadcast: 1 040 309 rx-pause: 0 rx-multicast: 486 321 rx-fcs-error: 0 rx-align-error: 0 rx-fragment: 0 rx-control: 0 rx-unknown-op: 0 rx-length-error: 0 rx-code-error: 0 rx-carrier-error: 0 rx-jabber: 0 rx-drop: 0 tx-bytes: 44 071 621 tx-packet: 312 597 tx-too-short: 0 tx-too-long: 8 397 tx-broadcast: 2 518 tx-pause: 2 112 tx-multicast: 7 142 tx-excessive-collision: 0 tx-multiple-collision: 0 tx-single-collision: 0 tx-excessive-deferred: 0 tx-deferred: 0 tx-late-collision: 0 tx-total-collision: 0 tx-drop: 0 tx-jabber: 0 tx-fcs-error: 0 tx-control: 2 112 tx-fragment: 0 tx-rx-64: 6 646 tx-rx-65-127: 1 509 891 tx-rx-128-255: 1 458 299 tx-rx-256-511: 178 975 tx-rx-512-1023: 953 tx-rx-1024-1518: 672 tx-rx-1519-max: 0

Some devices have multiple CPU cores that are directly connected to a built-in switch chip using separate data lanes. These devices can report which data lane was used to forward the packet from or to the CPU port from the switch chip. For such devices an extra line is added for each row, the first line represents data that was sent using the first data lane, the second line represents data that was sent using the second data line, and so on. You can find an example of the switch chip's statistics for a device with multiple data lanes connecting the CPU and the built-in switch chip:

[admin@MikroTik] > /interface ethernet switch print stats name: switch1 driver-rx-byte: 226 411 248 0 driver-rx-packet: 1 854 971 0 driver-tx-byte: 45 988 067 0 driver-tx-packet: 345 282 0 rx-bytes: 233 636 763 0 rx-packet: 1 855 018 0 rx-too-short: 0 0 rx-too-long: 0 0 rx-pause: 0 0 rx-fcs-error: 0 0 rx-overflow: 0 0 tx-bytes: 47 433 203 0 tx-packet: 345 282 0 tx-total-collision: 0 0

## <u>Setup Examples</u>

Make sure you have added all needed interfaces to the VLAN table when using secure vlan-mode. For routing functions to work properly on the same device through ports that use secure vlan-mode, you will need to allow access to the CPU from those ports, this can be done by adding the switchX-cpu interface itself to the VLAN table. Examples can be found in the Management port section.

It is possible to use the built-in switch chip and the CPU at the same time to create a Switch-Router setup, where a device acts as a switch and as a router at the same time. You can find a configuration example in the Switch-Router guide.

When allowing access to the CPU, you are allowing access from a certain port to the actual router/switch, this is not always desirable. Make sure you implement proper firewall filter rules to secure your device when access to the CPU is allowed from a certain VLAN ID and port, use firewall filter rules to allow access to only certain services.

Devices with MT7621, MT7531, EN7523, RTL8367, 88E6393X, 88E6191X, 88E6190 switch chips support HW offloaded vlan-filtering in RouterOS v7. VLAN-related configuration on the "/interface ethernet switch" menu is not available.

For VLAN related matchers or VLAN related action parameters to work on 88E6393X switch chip, you need to enable vlan-filtering on the bridge interface and make sure that hardware offloading is enabled on those ports, otherwise, these parameters will not have any effect..

VLAN Example 1 (Trunk and Access Ports)

RouterBOARDs with Atheros switch chips can be used for 802.1Q Trunking. This feature in RouterOS v6 is supported by  QCA8337, Atheros8316, Atheros8327, Atheros8227 and Atheros7240 switch chips. In this example, ether3, ether4, and ether5 interfaces are access ports, while ether2 is a trunk port. VLAN IDs for each access port: ether3 - 200, ether4 - 300, ether5 - 400.

Switch together the required ports:

/interface bridge add name=bridge1 /interface bridge port add bridge=bridge1 interface=ether2 hw=yes add bridge=bridge1 interface=ether3 hw=yes add bridge=bridge1 interface=ether4 hw=yes add bridge=bridge1 interface=ether5 hw=yes

By default, the bridge interface is configured with protocol-mode set to rstp. For some devices, this can disable hardware offloading because specific switch chips do not support this feature. See the Bridge Hardware Offloading section with supported features.

Add VLAN table entries to allow frames with specific VLAN IDs between ports:

/interface ethernet switch vlan add ports=ether2,ether3 switch=switch1 vlan-id=200 add ports=ether2,ether4 switch=switch1 vlan-id=300 add ports=ether2,ether5 switch=switch1 vlan-id=400

Assign vlan-mode and vlan-header mode for each port and also default-vlan-id on ingress for each access port:

/interface ethernet switch port set ether2 vlan-mode=secure vlan-header=add-if-missing set ether3 vlan-mode=secure vlan-header=always-strip default-vlan-id=200 set ether4 vlan-mode=secure vlan-header=always-strip default-vlan-id=300 set ether5 vlan-mode=secure vlan-header=always-strip default-vlan-id=400

Setting vlan-mode=secure ensures strict use of the VLAN table. Setting vlan-header=always-strip for access ports removes the VLAN header from the frame when it leaves the switch chip. Setting vlan-header=add-if-missing for trunk port adds VLAN header to untagged frames. default-vlan-id specifies what VLAN ID is added for untagged ingress traffic of the access port.

On QCA8337 and Atheros8327 switch chips, a default vlan-header=leave-as-is property should be used. The switch chip will determine which ports are access ports by using the default-vlan-id property. The default-vlan-id should only be used on access/hybrid ports to specify which VLAN the untagged ingress traffic is assigned to.

VLAN Example 2 (Trunk and Hybrid Ports)

VLAN Hybrid ports can forward both tagged and untagged traffic. This configuration is supported only by some Gigabit switch chips (QCA8337, Atheros8327).

Switch together the required ports:

/interface bridge add name=bridge1 /interface bridge port add bridge=bridge1 interface=ether2 hw=yes add bridge=bridge1 interface=ether3 hw=yes add bridge=bridge1 interface=ether4 hw=yes add bridge=bridge1 interface=ether5 hw=yes

By default, the bridge interface is configured with protocol-mode set to rstp. For some devices, this can disable hardware offloading because specific switch chips do not support this feature. See the Bridge Hardware Offloading section with supported features.

Add VLAN table entries to allow frames with specific VLAN IDs between ports.

/interface ethernet switch vlan add ports=ether2,ether3,ether4,ether5 switch=switch1 vlan-id=200 add ports=ether2,ether3,ether4,ether5 switch=switch1 vlan-id=300 add ports=ether2,ether3,ether4,ether5 switch=switch1 vlan-id=400

In the switch port menu set vlan-mode on all ports and also default-vlan-id on planned hybrid ports:

/interface ethernet switch port set ether2 vlan-mode=secure vlan-header=leave-as-is set ether3 vlan-mode=secure vlan-header=leave-as-is default-vlan-id=200 set ether4 vlan-mode=secure vlan-header=leave-as-is default-vlan-id=300 set ether5 vlan-mode=secure vlan-header=leave-as-is default-vlan-id=400

vlan-mode=secure will ensure strict use of the VLAN table. default-vlan-id will define VLAN for untagged ingress traffic on the port. In QCA8337 and Atheros8327 chips when vlan-mode=secure is used, it ignores switch port vlan-header options. VLAN table entries handle all the egress tagging/untagging and works as vlan-header=leave-as-is on all ports. It means what comes in tagged, goes out tagged as well, only default-vlan-id frames are untagged at the egress port.

### Management access configuration

In these examples, there will be shown examples for multiple scenarios, but each of these scenarios requires you to have switched ports. Below you can find how to switch multiple ports:

/interface bridge add name=bridge1 /interface bridge port add interface=ether1 bridge=bridge1 hw=yes add interface=ether2 bridge=bridge1 hw=yes

By default, the bridge interface is configured with protocol-mode set to rstp. For some devices, this can disable hardware offloading because specific switch chips do not support this feature. See the Bridge Hardware Offloading section with supported features.

In these examples, it will be assumed that ether1 is the trunk port and ether2 is the access port, for configuration as the following:

/interface ethernet switch port set ether1 vlan-header=add-if-missing set ether2 default-vlan-id=100 vlan-header=always-strip /interface ethernet switch vlan add ports=ether1,ether2,switch1-cpu switch=switch1 vlan-id=100

Tagged

To make the device accessible only from a certain VLAN, you need to create a new VLAN interface on the bridge interface and assign an IP address to it:

/interface vlan add name=MGMT vlan-id=99 interface=bridge1 /ip address add address=192.168.99.1/24 interface=MGMT

Specify from which interfaces it is allowed to access the device:

/interface ethernet switch vlan add ports=ether1,switch1-cpu switch=switch1 vlan-id=99

Only specify trunk ports in this VLAN table entry, it is not possible to allow access to the CPU with tagged traffic through an access port since the access port will tag all ingress traffic with the specified default-vlan-id value.

When the VLAN table is configured, you can enable vlan-mode=secure to limit access to the CPU:

/interface ethernet switch port set ether1 vlan-header=add-if-missing vlan-mode=secure set ether2 default-vlan-id=100 vlan-header=always-strip vlan-mode=secure set switch1-cpu vlan-header=leave-as-is vlan-mode=secure

Untagged

To make the device accessible from the access port, create a VLAN interface with the same VLAN ID as set in default-vlan-id, for example, VLAN 100, and add an IP address to it:

/interface vlan add name=VLAN100 vlan-id=100 interface=bridge1 /ip address add address=192.168.100.1/24 interface=VLAN100

Specify which access (untagged) ports are allowed to access the CPU:

/interface ethernet switch vlan add ports=ether1,ether2,switch1-cpu switch=switch1 vlan-id=100

Most commonly an access (untagged) port is accompanied by a trunk (tagged) port. In case of untagged access to the CPU, you are forced to specify both the access port and the trunk port, this gives access to the CPU from the trunk port as well. Not always this is desired and a Firewall might be required on top of VLAN filtering.

When the VLAN table is configured, you can enable vlan-mode=secure to limit access to the CPU:

/interface ethernet switch port set ether1 vlan-header=add-if-missing vlan-mode=secure set ether2 default-vlan-id=100 vlan-header=always-strip vlan-mode=secure set switch1-cpu vlan-header=leave-as-is vlan-mode=secure

To setup the management port using untagged traffic on a device with the Atheros7240 switch chip, you will need to set vlan-header=add- if-missing for the CPU port.

Untagged from tagged port

It is possible to allow access to the device from the trunk (tagged) port with untagged traffic. To do so, assign an IP address on the bridge interface:

/ip address add address=10.0.0.1/24 interface=bridge1

Specify which ports are allowed to access the CPU. Use vlan-id that is used in default-vlan-id for switch-cpu and trunk ports, by default it is set to 0 or 1.

/interface ethernet switch vlan add ports=ether1,switch1-cpu switch=switch1 vlan-id=1

When the VLAN table is configured, you can enable vlan-mode=secure to limit access to the CPU:

/interface ethernet switch port set ether1 default-vlan-id=1 vlan-header=add-if-missing vlan-mode=secure set switch1-cpu default-vlan-id=1 vlan-header=leave-as-is vlan-mode=secure

This configuration example is not possible for devices with the Atheros8316 and Atheros7240 switch chips. For devices with QCA8337 and Ather os8327 switch chips, it is possible to use any other default-vlan-id as long as it stays the same on switch-cpu and trunk ports. For devices with Atheros8227 switch chip only default-vlan-id=0 can be used and the trunk port must use vlan-header=leave-as-is.

### Inter-VLAN routing

Many MikroTik's devices come with a built-in switch chip that can be used to greatly improve overall throughput when configured properly. Devices with a switch chip can be used as a router and a switch at the same time, this gives you the possibility to use a single device instead of multiple devices for your network.

For this type of setup to work, you must switch all required ports together

/interface bridge add name=bridge1 /interface bridge port add bridge=bridge1 interface=ether2 hw=yes add bridge=bridge1 interface=ether3 hw=yes

Create a VLAN interface for each VLAN ID and assign an IP address to it:

/interface vlan add interface=bridge1 name=VLAN10 vlan-id=10 add interface=bridge1 name=VLAN20 vlan-id=20 /ip address add address=192.168.10.1/24 interface=VLAN10 add address=192.168.20.1/24 interface=VLAN20

Setup a DHCP Server for each VLAN:

/ip pool add name=POOL10 ranges=192.168.10.100-192.168.10.200 add name=POOL20 ranges=192.168.20.100-192.168.20.200 /ip dhcp-server add address-pool=POOL10 disabled=no interface=VLAN10 name=DHCP10 add address-pool=POOL20 disabled=no interface=VLAN20 name=DHCP20 /ip dhcp-server network add address=192.168.10.0/24 dns-server=8.8.8.8 gateway=192.168.10.1 add address=192.168.20.0/24 dns-server=8.8.8.8 gateway=192.168.20.1

Enable NAT on the device:

/ip firewall nat add action=masquerade chain=srcnat out-interface=ether1

Add each port to the VLAN table and allow these ports to access the CPU to make DHCP and routing work:

/interface ethernet switch vlan add independent-learning=yes ports=ether2,switch1-cpu switch=switch1 vlan-id=10 add independent-learning=yes ports=ether3,switch1-cpu switch=switch1 vlan-id=20

Specify each port to be an access port, and enable secure VLAN mode on each port and on the switch1-cpu port:

/interface ethernet switch port set ether2 default-vlan-id=10 vlan-header=always-strip vlan-mode=secure set ether3 default-vlan-id=20 vlan-header=always-strip vlan-mode=secure set switch1-cpu vlan-mode=secure

On QCA8337 and Atheros8327 switch chips, a default vlan-header=leave-as-is property should be used. The switch chip will determine which ports are access ports by using the default-vlan-id property. The default-vlan-id should only be used on access/hybrid ports to specify which VLAN the untagged ingress traffic is assigned to.

If your device has a switch rule table, then you can limit access between VLANs on a hardware level. As soon as you add an IP address on the VLAN interface you enable inter-VLAN routing, but this can be limited on a hardware level while preserving DHCP Server and other router-related services. To do so, use these ACL rules. With this type of configuration, you can achieve isolated port groups using VLANs.

/interface ethernet switch rule add dst-address=192.168.20.0/24 new-dst-ports="" ports=ether2 switch=switch1 add dst-address=192.168.10.0/24 new-dst-ports="" ports=ether3 switch=switch1

## See also

Switch Router Basic VLAN Switching Bridge Hardware Offloading Spanning Tree Protocol DHCP Snooping and Option 82 MTU on RouterBOARD Layer2 misconfiguration Master-port
