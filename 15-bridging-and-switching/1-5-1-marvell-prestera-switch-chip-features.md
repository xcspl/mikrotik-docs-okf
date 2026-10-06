---
type: Reference
title: "Marvell Prestera switch chip features"
description: "This article applies only to MikroTik devices with Marvell Prestera switch, not to CRS1xx/CRS2xx series switches."
timestamp: '2026-10-06'
status: active
tags: [routeros, mikrotik, networking]
resource: ~/Downloads/ROS-260526-1445-796.pdf
sources:
  - resource: https://manual.mikrotik.com/docs/introduction/
---

# Marvell Prestera switch chip features

Summary Features Models Abbreviations Port switching VLAN VLAN Filtering Port-Based VLAN MAC Based VLAN Protocol Based VLAN VLAN Tunneling (Q-in-Q) Ingress VLAN translation (R/M)STP Bonding Configuration example-VLANs with bonds Configure bonding Configure port switching Configure management IP Configure invalid VLAN filtering Configure InterVLAN routing Configure DHCP server Configure jumbo frames Multi-chassis Link Aggregation Group L3 Hardware Offloading Port isolation IGMP/MLD Snooping DHCP Snooping and DHCP Option 82 DHCPv6 Snooping and DHCP Option 18, Option 37 RA Guard Mirroring Configuration examples Port Based Mirroring VLAN Based Mirroring MAC Based Mirroring IP Based Mirroring Remote Switch Port Analyzer Property Reference Traffic Shaping Traffic Storm Control MPLS hardware offloading Switch Rules (ACL) Port Security Dual Boot Configuring SwOS using RouterOS See also

## <u>Summary</u>

Some MikroTik devices use high-performance and feature-rich Marvell Prestera Ethernet switches. These devices can be designed into various Ethernet applications including unmanaged switch, Layer 2 managed switch, carrier switch, inter-VLAN router, and wired unified packet processor.

This article applies only to MikroTik devices with Marvell Prestera switch, not to CRS1xx/CRS2xx series switches.

Features

Features Description

Forwarding Configurable ports for switching or routing Full non-blocking wire-speed switching Large Unicast FDB for Layer 2 unicast forwarding Forwarding Databases works based on IVL Jumbo frame support IGMP/MLD Snooping support DHCP Snooping support with custom Option 82 (Circuit ID, Remote ID) DHCPv6 Snooping support with custom Option 18 (Interface ID) and Option 37 (Remote ID) RA Guard support

Routing Layer 3 Hardware Offloading: IPv4, IPv6 Unicast Routing Supported on Ethernet, Bridge, Bonding, and VLAN interfaces ECMP Blackholes Offloaded Fasttrack connections 1 Offloaded NAT for Fasttrack connections 1 Multiple MTU profiles

1. Applies only to certain switch models
Spanning Tree Protocol STP RSTP MSTP Edge port, BPDU Guard, Root Guard

Mirroring Various types of mirroring: Port based mirroring VLAN based mirroring MAC based mirroring Remote Switch Port Analyzer (RSPAN)

VLAN Fully compatible with IEEE802.1Q and IEEE802.1ad VLAN 4k active VLANs Flexible VLAN assignment: Port based VLAN Protocol based VLAN MAC based VLAN VLAN filtering Ingress VLAN translation Multiple VLAN Registration protocol (MVRP)

Bonding Supports 802.3ad (LACP), balance-xor and active-backup modes Up to 8 member ports per bonding interface Hardware automatic failover and load balancing MLAG

Quality of Service (QoS) Eight output queues per port DSCP and 802.1p PCP mapping Port based Layer2 and Layer3 trust settings Port and Queue based egress rate limiter Policy based QoS via ACL rules Strict Priority (SP) and Shaped Deficit Weighted Round Robin (SDWRR) queuing Enhanced Transmission Selection (ETS) scheduling Weighted Random Early Detection (WRED) 1 Explicit Congestion Notification (ECN) 1 Priority-based Flow Control (PFC) 1 Resource allocation control (queue, shared-pool and multicast based) with extensive monitoring capabilities Compatible with Dante enviroments Compatible with RDMA over Converged Ethernet (RoCE) enviroment 1 Ingress traffic limiting (port based or via ACL rules) Traffic storm control

1. Applies only to certain switch models
Port isolation Applicable for Private VLAN implementation

Access Control List Ingress ACL tables Classification based on ports, L2, L3, L4 protocol header fields ACL actions include filtering, forwarding and modifying of the protocol header fields

PTP Two-step Ordinary Clock and Boundary Clock. Hardware timestamping, ensuring clock syncronization in nanosecond(ns) range. IPv4 and Layer 2 (L2) multicast transport modes. End-to-End (E2E) and Peer-to-Peer (P2P) delay mechanisms. IEEE 1588-2008 (PTPv2). Profile Support for:

802.1AS: Timing and synchronization for Audio Video Bridging (AVB) and Time-Sensitive Networking (TSN). AES67: High-performance audio-over-IP interoperability.
G.8275.1: Frequency and phase synchronization in PTP-aware networks. SMPTE: Audio/video synchronization in professional broadcast environments.
PTP support is hardware-dependent, please refer to the list of supported devices.

For L3 hardware offloading feature support and hardware limits, please refer to Feature Support and Device Support user manuals.

For QoS hardware offloading feature support and hardware limits, please refer to Quality of Service (QoS) user manuals.

Models

This table clarifies the main differences between Cloud Router Switch models and CCR routers.

Model Switch Chip CPU Size of Ethernet PoE out ACL Unicast FDB Jumbo Frame RAM rules entries (Bytes) CRS318-1Fi-15Fr-2S-OUT (netPower Marvell-ARM 2-core 800MHz 256 MB 16x 10/100M Ethernet 1x passive up to 16K 10218 15FR) 98DX224S 2x 1G SFP

|CRS318-16P-2S+OUT (netPower|Marvell-|ARM 2-core 800MHz|256 MB|16x 10/100/1000M Ethernet|16x 802.3af|128|up to 16K|10218|
|---|---|---|---|---|---|---|---|---|
|16P)|98DX226S|||2x 10G SFP+|/at||||
|CRS310-1G-5S-4S+ (netFiber 9/IN)|Marvell- 98DX226S|ARM 2-core 800MHz|256 MB|1x 10/100/1000M Ethernet 5x 1G SFP 4x 10G SFP+||128|up to 16K|10218|
|CRS310-8G+2S+IN|Marvell- 98DX226S|ARM 2-core 800MHz|256 MB|8x 2.5G Ethernet 2x 10G SFP+||128|up to 16K|10218|
|CRS320-8P-8B-4S+RM|Marvell- 98DX226S|ARM 2-core 800MHz|256 MB|16x 10/100/1000M Ethernet 4x 10G SFP+|8x 802.3af /at 8x 802.3bt|128|up to 16K|10218|
|CRS304-4XG-IN|Marvell-|ARM64 2-core|512 MB|4x 1/2.5/5/10G Ethernet||128|up to 16K|10218|
||98DX2528|1200MHz|||||||
|CRS326-24G-2S+ (RM/IN)|Marvell- 98DX3236|ARM 2-core 800MHz|512 MB|24x 10/100/1000M Ethernet 2x 10G SFP+||128|up to 16K|10218|
|CRS328-24P-4S+RM|Marvell- 98DX3236|ARM 1-core 800MHz|512 MB|24x 10/100/1000M Ethernet 4x 10G SFP+|24x 802.3af /at|128|up to 16K|10218|
|CRS328-4C-20S-4S+RM|Marvell- 98DX3236|ARM 2-core 800MHz|512 MB|20x 1G SFP 4x 1G combo 4x 10G SFP+||128|up to 16K|10218|
|CRS305-1G-4S+IN|Marvell- 98DX3236|ARM 2-core 800MHz|512 MB|1x 10/100/1000M Ethernet 4x 10G SFP+||128|up to 16K|10218|
|CRS305-1G-4S+OUT (FiberBox Plus)|Marvell- 98DX226S|ARM 2-core 800MHz|256 MB|1x 10/100/1000M Ethernet 4x 10G SFP+||128|up to 16K|10218|
|CRS309-1G-8S+IN|Marvell- 98DX8208|ARM 2-core 800MHz|512 MB|1x 10/100/1000M Ethernet 8x 10G SFP+||1024|up to 32K|10218|
|CRS317-1G-16S+RM|Marvell- 98DX8216|ARM 2-core 800MHz|1 GB|1x 10/100/1000M Ethernet 16x 10G SFP+||1024|up to 128K|10218|
|CRS312-4C+8XG-RM|Marvell-|MIPSBE 1-core|64 MB|4x 10G combo||512|up to 32K|10218|
||98DX8212|650MHz||8x 1/2.5/5/10G Ethernet|||||
|CRS326-24S+2Q+RM|Marvell-|MIPSBE 1-core|128 MB|24x 10G SFP+||256|up to 32K|10218|
||98DX8332|650MHz||2x 40G QSFP+|||||
|CRS326-4C+20G+2Q+RM|Marvell-|MIPSBE 1-core|128 MB|4x 2.5G Ethernet/10G SFP+||256|up to 32K|10218|
||98DX8332|650MHz||combo 20x 2.5G Ethernet 2x 40G QSFP+|||||
|CRS354-48G-4S+2Q+RM|Marvell-|MIPSBE 1-core|128 MB|48x 10/100/1000M Ethernet||170|up to 32K|10218|
||98DX3257|650MHz||4x 10G SFP+ 2x 40G QSFP+|||||
|CRS354-48P-4S+2Q+RM|Marvell-|MIPSBE 1-core|128 MB|48x 10/100/1000M Ethernet|48x 802.3af|170|up to 32K|10218|
||98DX3257|650MHz||4x 10G SFP+ 2x 40G QSFP+|/at||||
|CRS418-8P-8G-2S+RM|Marvell-|ARM64 4-core|1 GB|16x 10/100/1000M Ethernet|8x 802.3af|128|up to 16K|10218|
|CRS418-8P-8G-2S+5axQ2axQ-RM|98DX226S|2208MHz||2x 10G SFP+|/at||||
|CRS504-4XQ (IN/OUT)|Marvell-|MIPSBE 1-core|64 MB|4x 100G QSFP28||1024|up to 128K|10218|
||98DX4310|650MHz|||||||
|CRS510-8XS-2XQ-IN|Marvell-|MIPSBE 1-core|128 MB|8x 25G SFP28||1024|up to 128K|10218|
||98DX4310|650MHz||2x 100G QSFP28|||||

CRS518-16XS-2XQ-RM Marvell-MIPSBE 1-core 64 MB 16x 25G SFP28 up to 128K 10218 98DX8525 650MHz 2x 100G QSFP28 CRS520-4XS-16XQ-RM Marvell-ARM64 4-core 4 GB 4x 25G SFP28 682 up to 256K 9570 98CX8410 2000MHz 16x 100G QSFP28 CRS812-8DS-2DQ-2DDQ-RM Marvell-ARM64 4-core 4 GB 8x 50G SFP56 1365 up to 128K 9570 98DX7335 2000MHz 2x 200G QSFP56 2x 400G QSFP56-DD CRS804-4DDQ-hRM Marvell-ARM64 4-core 4 GB 4x 400G QSFP56-DD 1365 up to 128K 9570 98DX7335 2000MHz CCR2116-12G-4S+ Marvell-ARM64 16-core 16 GB 12x 10/100/1000M Ethernet 512 up to 32K 9570 98DX3255 2000MHz 4x 10G SFP+ CCR2216-1G-12XS-2XQ Marvell-ARM64 16-core 16 GB 12x 25G SFP28 1024 up to 128K 9570 98DX8525 2000MHz 2x 100G QSFP28 RDS2216-2XG-4S+4XS-2XQ Marvell-ARM64 16-core 32 GB 2x 1/2.5/5/10G Ethernet 1024 up to 128K 9570 98DX4310 2000MHz 4x 10G SFP+ 4x 25G SFP28 2x 100G QSFP28

Abbreviations

FDB-Forwarding Database MDB-Multicast Database SVL-Shared VLAN Learning IVL-Independent VLAN Learning PVID-Port VLAN ID ACL-Access Control List CVID-Customer VLAN ID SVID-Service VLAN ID

## <u>Port switching</u>

In order to set up a port switching, check the Bridge Hardware Offloading page.

Currently, it is possible to create only one bridge with hardware offloading. Use the hw=yes/no parameter to select which bridge will use hardware offloading.

Bridge STP/RSTP/MSTP, IGMP Snooping and VLAN filtering settings don't affect hardware offloading, since RouterOS v6.42 Bonding interfaces are also hardware offloaded.

## <u>VLAN</u>

Since RouterOS version 6.41, a bridge provides VLAN aware Layer2 forwarding and VLAN tag modifications within the bridge. This set of features makes bridge operation more like a traditional Ethernet switch and allows to overcome Spanning Tree compatibility issues compared to the configuration when tunnel-like VLAN interfaces are bridged. Bridge VLAN Filtering configuration is highly recommended to comply with STP (802.1D), RSTP (802.1w) standards and it is mandatory to enable MSTP (802.1s) support in RouterOS.

### VLAN Filtering

VLAN filtering is described on the Bridge VLAN Filtering section.

## VLAN setup examples

Below are describes some of the most common ways how to utilize VLAN forwarding.

Port-Based VLAN

The configuration is described on the Bridge VLAN FIltering section.

MAC Based VLAN

The Switch Rule table is used for MAC Based VLAN functionality, see this table on how many rules each device supports. MAC-based VLANs will only work properly between switch ports and not between switch ports and CPU. When a packet is being forwarded to the CPU, the pvid property for the bridge port will be always used instead of new-vlan-id from ACL rules. MAC-based VLANs will not work for DHCP packets when DHCP snooping is enabled.

Enable switching on ports by creating a bridge with enabled hw-offloading:

/interface bridge add name=bridge1 vlan-filtering=yes /interface bridge port add bridge=bridge1 interface=ether2 hw=yes add bridge=bridge1 interface=ether7 hw=yes

Add VLANs in the Bridge VLAN table and specify ports:

/interface bridge vlan add bridge=bridge1 tagged=ether2 untagged=ether7 vlan-ids=200,300,400

Add Switch rules which assign VLAN id based on MAC address:

/interface ethernet switch rule add switch=switch1 ports=ether7 src-mac-address=A4:12:6D:77:94:43/FF:FF:FF:FF:FF:FF new-vlan-id=200 add switch=switch1 ports=ether7 src-mac-address=84:37:62:DF:04:20/FF:FF:FF:FF:FF:FF new-vlan-id=300 add switch=switch1 ports=ether7 src-mac-address=E7:16:34:A1:CD:18/FF:FF:FF:FF:FF:FF new-vlan-id=400

Protocol Based VLAN

The Switch Rule table is used for Protocol Based VLAN functionality, see this table on how many rules each device supports. Protocol-based VLANs will only work properly between switch ports and not between switch ports and CPU. When a packet is being forwarded to the CPU, the pvid property for the bridge port will be always used instead of new-vlan-id from ACL rules. Protocol-based VLANs will not work for DHCP packets when DHCP snooping is enabled.

Enable switching on ports by creating a bridge with enabled hw-offloading:

/interface bridge add name=bridge1 vlan-filtering=yes /interface bridge port add bridge=bridge1 interface=ether2 hw=yes add bridge=bridge1 interface=ether6 hw=yes add bridge=bridge1 interface=ether7 hw=yes add bridge=bridge1 interface=ether8 hw=yes

Add VLANs in the Bridge VLAN table and specify ports:

/interface bridge vlan add bridge=bridge1 tagged=ether2 untagged=ether6 vlan-ids=200 add bridge=bridge1 tagged=ether2 untagged=ether7 vlan-ids=300 add bridge=bridge1 tagged=ether2 untagged=ether8 vlan-ids=400

Add Switch rules which assign VLAN id based on MAC protocol:

/interface ethernet switch rule add mac-protocol=ip new-vlan-id=200 ports=ether6 switch=switch1 add mac-protocol=ipx new-vlan-id=300 ports=ether7 switch=switch1 add mac-protocol=0x80F3 new-vlan-id=400 ports=ether8 switch=switch1

VLAN Tunneling (Q-in-Q)

Since RouterOS v6.43 it is possible to use a provider bridge (IEEE 802.1ad) and Tag Stacking VLAN filtering, and hardware offloading at the same time. The configuration is described in the Bridge VLAN Tunneling (Q-in-Q) section.

Devices with switch chip Marvell-98DX3257 (e.g. CRS354 series) do not support VLAN filtering on 1Gbps Ethernet interfaces for other VLAN types (0x88a8 and 0x9100).

### Ingress VLAN translation

It is possible to translate a certain VLAN ID to a different VLAN ID using ACL rules on an ingress port. In this example we create two ACL rules, allowing bidirectional communication. This can be done by doing the following.

Create a new bridge and add ports to it with hardware offloading:

/interface bridge add name=bridge1 vlan-filtering=no /interface bridge port add interface=ether1 bridge=bridge1 hw=yes add interface=ether2 bridge=bridge1 hw=yes

Add ACL rules to translate a VLAN ID in each direction:

/interface ethernet switch rule add new-dst-ports=ether2 new-vlan-id=20 ports=ether1 switch=switch1 vlan-id=10 add new-dst-ports=ether1 new-vlan-id=10 ports=ether2 switch=switch1 vlan-id=20

Add both VLAN IDs to the bridge VLAN table:

/interface bridge vlan add bridge=bridge1 tagged=ether1 vlan-ids=10 add bridge=bridge1 tagged=ether2 vlan-ids=20

Enable bridge VLAN filtering:

/interface bridge set bridge1 vlan-filtering=yes

Bidirectional communication is limited only between two switch ports. Translating VLAN ID between more ports can cause traffic flooding or incorrect forwarding between the same VLAN ports.

By enabling vlan-filtering you will be filtering out traffic destined to the CPU, before enabling VLAN filtering you should make sure that you set up a Management port.

## <u>(R/M)STP</u>

MikroTik devices with Marvell Prestera switch are capable of running STP, RSTP, and MSTP on a hardware level. For more detailed information you should check out the Spanning Tree Protocol manual page and for relevant configuration/monitoring options see the Bridging and Switching page.

## <u>Bonding</u>

MikroTik devices with Marvell Prestera switch support hardware offloading with bonding interfaces. Only 802.3ad (LACP), balance-xor (static LAG) and active-backup bonding modes are hardware offloaded, other bonding modes will use the CPU's resources. You can find more information about the bonding interfaces in the Bonding Interface section.

To create a hardware offloaded bonding interface, you must create a bonding interface with a supported bonding mode:

/interface bonding add mode=802.3ad name=bond1 slaves=ether1,ether2

This interface can be added to a bridge alongside other interfaces:

/interface bridge add name=bridge /interface bridge port add bridge=bridge interface=bond1 hw=yes add bridge=bridge interface=ether3 hw=yes add bridge=bridge interface=ether4 hw=yes

Do not add interfaces to a bridge that are already in a bond, RouterOS will not allow you to add an interface to bridge that is already a slave port for bonding.

Make sure that the bonding interface is hardware offloaded by checking the "H" flag:

/interface bridge port print Flags: X-disabled, I-inactive, D-dynamic, H-hw-offload # INTERFACE BRIDGE HW 0 H bond1 bridge yes 1 H ether3 bridge yes 2 H ether4 bridge yes

With HW-offloaded bonding interfaces, the built-in switch chip will always use Layer2+Layer3+Layer4 for a transmit hash policy, changing the transmit hash policy manually will have no effect.

### Configuration example-VLANs with bonds

This section will show how to configure multiple switches to use bonding interfaces and port-based VLANs, it will also show a working example with a DHCP-Server, inter-VLAN routing, management IP, and invalid VLAN filtering configuration.

For this network topology, we will be using two CRS326-24G-2S+, one CRS317-1G-16S+, and one CCR1072-1G-8S+.

In this setup, SwitchA and SwitchC will tag all traffic from ports ether1-ether8 to VLAN ID 10, ether9-ether16 to VLAN ID 20, and ether17-ether24 to VLAN ID 30. Management will only be possible if a user is connecting with tagged traffic with VLAN ID 99 from ether1 on SwitchA or SwitchB, connecting to all devices will also be possible from the router using tagged traffic with VLAN ID 99. The SFP+ ports in this setup are going to be used as VLAN trunk ports while being in a bond to create a LAG interface.

Configure bonding

Bonding interfaces are used when a larger amount of bandwidth is required, this is done by creating a link aggregation group, which also provides hardware automatic failover and load balancing for switches. By adding two 10Gbps interfaces to bonding, you can increase the theoretical bandwidth limit to 20Gbps. Make sure that all bonded interfaces are linked to the same speed rates.

e-offloaded bridge, the switches aggregate traffic using the built-in switch chip without using CPU resources.When using the hardwar

To create a 20Gbps bonding interface from sfp-sfpplus1 and sfp-sfpplus2 between SwitchA to SwitchB and between SwitchC to SwitchB, use these commands on SwitchA and SwitchC:

/interface bonding add mode=802.3ad name=bond_1-2 slaves=sfp-sfpplus1,sfp-sfpplus2

To create a 40Gbps bonding interface between SwitchB and the Router and a 20Gbps bonding interface between SwitchA and SwitchC, use these commands on SwitchB:

/interface bonding add mode=802.3ad name=bond_1-2 slaves=sfp-sfpplus1,sfp-sfpplus2 add mode=802.3ad name=bond_3-4 slaves=sfp-sfpplus3,sfp-sfpplus4 add mode=802.3ad name=bond_5-6-7-8 slaves=sfp-sfpplus5,sfp-sfpplus6,sfp-sfpplus7,sfp-sfpplus8

In our case the Router needs a software-based bonding interface, use these commands on Router: the

/interface bonding add mode=802.3ad name=bond_1-2-3-4 slaves=sfp-sfpplus1,sfp-sfpplus2,sfp-sfpplus3,sfp-sfpplus4

Interface bonding does not create an interface with a larger link speed. Interface bonding creates a virtual interface that can load balance traffic over multiple interfaces. More details can be found on the LAG interfaces and load balancing page.

Configure port switching

All switches in this setup require that all used ports are switched together. For bonding, you should add the bonding interface as a bridge port, instead of individual bonding ports. Use these commands on SwitchA and SwitchC:

/interface bridge add name=bridge vlan-filtering=no /interface bridge port add bridge=bridge interface=ether1 pvid=10 add bridge=bridge interface=ether2 pvid=10 add bridge=bridge interface=ether3 pvid=10 add bridge=bridge interface=ether4 pvid=10 add bridge=bridge interface=ether5 pvid=10 add bridge=bridge interface=ether6 pvid=10 add bridge=bridge interface=ether7 pvid=10 add bridge=bridge interface=ether8 pvid=10 add bridge=bridge interface=ether9 pvid=20 add bridge=bridge interface=ether10 pvid=20 add bridge=bridge interface=ether11 pvid=20 add bridge=bridge interface=ether12 pvid=20 add bridge=bridge interface=ether13 pvid=20 add bridge=bridge interface=ether14 pvid=20 add bridge=bridge interface=ether15 pvid=20 add bridge=bridge interface=ether16 pvid=20 add bridge=bridge interface=ether17 pvid=30 add bridge=bridge interface=ether18 pvid=30 add bridge=bridge interface=ether19 pvid=30 add bridge=bridge interface=ether20 pvid=30 add bridge=bridge interface=ether21 pvid=30 add bridge=bridge interface=ether22 pvid=30 add bridge=bridge interface=ether23 pvid=30 add bridge=bridge interface=ether24 pvid=30 add bridge=bridge interface=bond_1-2

Add all bonding interfaces to a single bridge on SwitchB by using these commands on SwitchB:

/interface bridge add name=bridge vlan-filtering=no /interface bridge port add bridge=bridge interface=bond_1-2 add bridge=bridge interface=bond_3-4 add bridge=bridge interface=bond_5-6-7-8

Configure management IP

It is very useful to create a management interface and assign an IP address to it to preserve access to the switch. This is also very useful when updating your switches since such traffic to the switch will be blocked when enabling invalid VLAN filtering.

Create a routable VLAN interface on SwitchA, SwitchB, and SwitchC:

/interface vlan add interface=bridge name=MGMT vlan-id=99

The Router needs a routable VLAN interface to be created on the bonding interface, use these commands to create a VLAN interface on Router: the

|/interface vlan||add interface=bond_1-2-3-4 name=MGMT vlan-id=99 For this guide, we are going to use these addresses for each device:|
|---|---|---|
|Device|Address||
|Router SwitchA SwitchB SwitchC|192.168.99.1 192.168.99.2 192.168.99.3 192.168.99.4|Add an IP address for each switch device on the VLAN interface (change X to the appropriate number):|
|/ip address||add address=192.168.99.X/24 interface=MGMT Do not forget to add the default gateway and specify a DNS server on the switch devices:|
|/ip route /ip dns|add gateway=192.168.99.1 set servers=192.168.99.1 Add the IP address on the Router:||
|/ip address||add address=192.168.99.1/24 interface=MGMT|
||Configure invalid VLAN filtering /interface bridge port /interface bridge port /interface bridge port witchA, SwitchB and SwitchC:|Since most ports on SwitchA and SwitchC are going to be access ports, you can set all ports to accept only certain types of packets, in this case, we will want SwitchA and SwitchC to only accept untagged packets, use these commands on SwitchA and SwitchC: set [find] frame-types=admit-only-untagged-and-priority-tagged There is an exception for frame types on SwitchA and SwitchC, in this setup access to the management is required from ether1 and bonding interfaces, they require that tagged traffic can be forwarded. Use these commands on SwitchA and SwitchC: set [find where interface=ether1] frame-types=admit-all set [find where interface=bond_1-2] frame-types=admit-only-vlan-tagged On SwitchB only tagged packets should be forwarded, use these commands on SwitchB: set [find] frame-types=admit-only-vlan-tagged An optional step is to set frame-types=admit-only-vlan-tagged on the bridge interface to disable the default untagged VLAN 1 (pvid=1). We are using the tagged VLAN on the bridge for management access, so there is no need to accept untagged traffic on the bridge. Use these commands on the S|

/interface bridge set [find name=bridge] frame-types=admit-only-vlan-tagged

It is required to set up a bridge VLAN table. In this network setup, we need to allow VLAN 10 on ether1-ether8, VLAN 20 on ether9-ether16, VLAN 30 on ether17-ether24, VLAN 10,20,30,99 on bond_1-2, and a special case for ether1 to allow to forward VLAN 99 on SwitchA and SwitchC. Use these commands on SwitchA and SwitchC:

/interface bridge vlan add bridge=bridge tagged=bond_1-2 vlan-ids=10 add bridge=bridge tagged=bond_1-2 vlan-ids=20 add bridge=bridge tagged=bond_1-2 vlan-ids=30 add bridge=bridge tagged=bridge,bond_1-2,ether1 vlan-ids=99

Bridge ports with frame-types set to admit-all oradmit-only-untagged-and-priority-tagged will be automatically added as untagged ports for the pvid VLAN.

Similarly, it is required to set up a bridge VLAN table for SwitchB. Use these commands on SwitchB:

/interface bridge vlan add bridge=bridge tagged=bond_1-2,bond_3-4,bond_5-6-7-8 vlan-ids=10,20,30 add bridge=bridge tagged=bond_1-2,bond_3-4,bond_5-6-7-8,bridge vlan-ids=99

When everything is configured, VLAN filtering can be enabled. Use these commands on SwitchA, SwitchB, and SwitchC:

/interface bridge set bridge vlan-filtering=yes

Double-check if port-based VLANs are set up properly. If a mistake was made, you might lose access to the switch and it can only be regained by resetting the configuration or by using the serial console.

VLAN filtering is described more in the Bridge VLAN Filtering section.

Configure InterVLAN routing

To create InterVLAN routing, the VLAN interface for each customer VLAN ID must be created on the router and must have an IP address assigned to it. The VLAN interface must be created on the bonding interface created previously.

Use these commands on the Router:

/interface vlan add interface=bond_1-2-3-4 name=VLAN10 vlan-id=10 add interface=bond_1-2-3-4 name=VLAN20 vlan-id=20 add interface=bond_1-2-3-4 name=VLAN30 vlan-id=30 /ip address add address=192.168.10.1/24 interface=VLAN10 add address=192.168.20.1/24 interface=VLAN20 add address=192.168.30.1/24 interface=VLAN30

These commands are required for DHCP-Server. In case interVLAN routing is not desired but a DHCP-Server on a single router is required, then use Firewall Filter to block access between different subnets.

Since RouterOS v7, it is possible to route traffic using the L3 HW offloading on certain devices. See more details on L3 Hardware Offloading.

Configure DHCP server

To get the DHCP-Server working for each VLAN ID, the server must be set up on the previously created VLAN interfaces (one server for each VLAN ID). Preferably each VLAN ID should have its own subnet and its own IP pool. A DNS Server could be specified as the router's IP address for a particular VLAN ID or a global DNS Server could be used, but this address must be reachable.

To set up the DHCP-Server, use these commands on the Router:

/ip pool add name=VLAN10_POOL ranges=192.168.10.100-192.168.10.200 add name=VLAN20_POOL ranges=192.168.20.100-192.168.20.200 add name=VLAN30_POOL ranges=192.168.30.100-192.168.30.200 /ip dhcp-server add address-pool=VLAN10_POOL disabled=no interface=VLAN10 name=VLAN10_DHCP add address-pool=VLAN20_POOL disabled=no interface=VLAN20 name=VLAN20_DHCP add address-pool=VLAN30_POOL disabled=no interface=VLAN30 name=VLAN30_DHCP /ip dhcp-server network add address=192.168.10.0/24 dns-server=192.168.10.1 gateway=192.168.10.1 add address=192.168.20.0/24 dns-server=192.168.20.1 gateway=192.168.20.1 add address=192.168.30.0/24 dns-server=192.168.30.1 gateway=192.168.30.1

In case the router's DNS Server is being used, don't forget to allow remote requests and make sure DNS Servers are configured on the router. Use these commands on the Router:

/ip dns set allow-remote-requests=yes servers=8.8.8.8

Make sure to secure your local DNS Server with Firewall from the outside when using allow-remote-requests set to yes since your DNS Server can be used for DDoS attacks if it is accessible from the Internet by anyone.

Don't forget to create NAT, assuming that sfp-sfpplus8 is used as WAN port, use these commands on the Router:

/ip firewall nat add action=masquerade chain=srcnat out-interface=sfp-sfpplus8

Configure jumbo frames

One can increase the total throughput in such a setup by enabling jumbo frames. This reduces the packet overhead by increasing the Maximum Transmission Unit (MTU). If a device in your network does not support jumbo frames, then it will not benefit from a larger MTU. Usually, the whole network does not support jumbo frames, but you can still benefit when sending data between devices that support jumbo frames, including all switches in the path.

In this case, if clients behind SwitchA and client behind SwitchC support jumbo frames, then enabling jumbo frames will be beneficial. Before enabling jumbo frames, determine the MAX-L2MTU by using this command:

[admin@SwitchA] > interface print Flags: R-RUNNING Columns: NAME, TYPE, ACTUAL-MTU, L2MTU, MAX-L2MTU, MAC-ADDRESS # NAME TYPE ACTUAL-MTU L2MTU MAX-L2MTU MAC-ADDRESS 1 R sfp-sfpplus1 ether 1500 1584 10218 64:D1:54:FF:E3:7F

More information can be found in MTU manual page.

When MAX-L2MTU is determined, choose the MTU size depending on the traffic on your network, use this command on SwitchA, SwitchB, and SwitchC:

/interface ethernet set [ find] l2mtu=10218 mtu=10218

Don't forget to change the MTU on your client devices too, otherwise, the above-mentioned settings will not have any effect.

## Multi-chassis Link Aggregation Group

MLAG (Multi-chassis Link Aggregation Group) implementation in RouterOS allows configuring LACP bonds on two separate devices, while the client device believes to be connected on the same machine. This provides a physical redundancy in case of switch failure. MikroTik devices with Marvell Prestera switch can be configured with hardware offloaded MLAG. Read here for more information.

## L3 Hardware Offloading

Layer3 hardware offloading (otherwise known as IP switching or HW routing) will allow to offload some of the router features onto the switch chip. This allows reaching wire speeds when routing packets, which simply would not be possible with the CPU.

Offloaded feature set depends on the used chipset. Read here for more info.

## Port isolation

Since RouterOS v6.43 is it possible to create a Private VLAN setup, an example can be found in the Switch chip port isolation manual page. Hardware offloaded bonding interfaces are not included in the switch port-isolation menu, but it is still possible to configure port-isolation individually on each secondary interface of the bonding.

Port isolation can be used with vlan-filtering bridge and it is possible to isolate ports that are members of the same VLAN. The isolation works per-port, it is not possible to isolate ports per-VLAN.

## IGMP/MLD Snooping

MikroTik devices with Marvell Prestera switch are capable of using IGMP/MLD Snooping on a hardware level. To see more detailed information, you should check out the IGMP/MLD snooping manual page.

## DHCP Snooping and DHCP Option 82

MikroTik devices with Marvell Prestera switch are capable of using DHCP Snooping with custom Option 82 (Circuit ID, Remote ID) on a hardware level. The switch will create a dynamic ACL rule to capture the DHCP packets and redirect them to the main CPU for further processing. To see more detailed information, please visit the DHCP Snooping and DHCP Option 82 manual page.

Starting from RouterOS v7.17, DHCP snooping is supported with hardware offloading bonding interfaces.

## DHCPv6 Snooping and DHCP Option 18, Option 37

MikroTik devices with Marvell Prestera switch are capable of using DHCPv6 Snooping with custom Option 18 (Interface ID) and Option 37 (Remote ID) on a hardware level since RouterOS v7.23. The switch will create a dynamic ACL rule to capture the DHCPv6 packets and redirect them to the main CPU for further processing. To see more detailed information, please visit the DHCPv6 Snooping / DHCPv6 Shield manual page.

## RA Guard

MikroTik devices with Marvell Prestera switch are capable of using RA Guard on a hardware level since RouterOS v7.22. The switch will create a dynamic ACL rule to capture the relevant IPv6 packets and redirect them to the main CPU for further processing. To see more detailed information, please visit the RA Guard manual page.

## <u>Mirroring</u>

Mirroring is a function that allows a network switch to duplicate all the data passing through it and send a copy to another specified port, known as the mirr or-target. This feature is useful for setting up a tap device, which allows for analyzing network traffic using a separate device. You can set up mirroring in a simple way by designating source ports (see mirror-egress and mirror-ingress in /interface/ethernet/switch/port), or you can configure more advanced mirroring based on different criteria (see mirror in /interface/ethernet/switch/rule).

It is important to note that the mirror-target port must be on the same switch. You can check the device block diagram or navigate to the /interface /ethernet menu to identify which interfaces are connected where. When setting up the configration, it is not mandatory to add the mirror-target interface to the same hardware offloaded bridge where the source ports are set up. The mirror-target port can be a standalone interface (not configured as a bridge port), or it can be within a bridge setup. When using the mirror-target with a bridge, note that data and mirrored traffic may both travel on the same LAN. In such cases, consider employing RSPAN (Remote Switch Port Analyzer), where mirrored traffic is encapsulated into a separate VLAN before being transmitted over the network.

Additionally, you can set the mirror-target port to a special value "cpu", which means that the copied packets will be sent to the switch chip's CPU port.

### Configuration examples

Port Based Mirroring

Starting from RouterOS version 7.15, it is possible to configure multiple source ports and selectively choose whether to mirror incoming traffic, outgoing traffic, or both. In this example, both incoming and outgoing traffic from the ether2 interface will be copied and sent to the ether3 interface for monitoring or analysis.

# Since RouterOS v7.15 /interface ethernet switch port set ether2 mirror-egress=yes mirror-ingress=yes /interface ethernet switch set switch1 mirror-target=ether3

# Older RouterOS: /interface ethernet switch set switch1 mirror-source=ether2 mirror-target=ether3

VLAN Based Mirroring

Using ACL rules, it is possible to mirror packets from multiple interfaces using the ports setting. Additionally, you can specify more detailed criteria such as VLAN ID, MAC/IP address or TCP/UDP port. Only ingress packets are mirrored to mirror-target interface. This example will mirror incoming VLAN 11 traffic from the ether2 interface, and send copies to the ether3 interface. To use an ACL rule with a vlan-id matcher, you need to have bridge vlan- filtering enabled.

/interface bridge set bridge1 vlan-filtering=yes /interface ethernet switch set switch1 mirror-target=ether3 /interface ethernet switch rule add mirror=yes ports=ether1 switch=switch1 vlan-id=11

MAC Based Mirroring

This example will mirror incoming traffic with 64:D1:54:D9:27:E6 MAC destination or source address from the ether1 interface, and send copies to the ether3 interface.

|||/interface ethernet switch set switch1 mirror-target=ether3 /interface ethernet switch rule||add mirror=yes ports=ether1 switch=switch1 dst-mac-address=64:D1:54:D9:27:E6/FF:FF:FF:FF:FF:FF add mirror=yes ports=ether1 switch=switch1 src-mac-address=64:D1:54:D9:27:E6/FF:FF:FF:FF:FF:FF|
|---|---|---|---|---|
|interface.|IP Based Mirroring|/interface ethernet switch /interface ethernet switch rule Remote Switch Port Analyzer /interface ethernet switch port /interface ethernet switch|set ether2 mirror-egress=yes mirror-ingress=yes|This example will mirror incoming traffic with 192.168.88.0/24 IP destination or source address from the ether1 interface, and send copies to the ether3 set switch1 mirror-target=ether3 mirror-source=none add mirror=yes ports=ether1 switch=switch1 src-address=192.168.88.0/24 add mirror=yes ports=ether1 switch=switch1 dst-address=192.168.88.0/24 There are other options as well, check the ACL section to find out all possible parameters that can be used to match packets. This example will mirror incomming and outgoing traffic from the ether2 interface, copies will be encapsulated in 802.1Q VLAN using the 999 as VLAN ID, and packets will be sent to the ether3 interface. If the original traffic is already VLAN tagged, RSPAN will add another layer of VLAN tagging as an outer tag. This results in the mirrored traffic being tagged twice. If the mirror-target port is included in vlan-filtering bridge, it is not required to make the interface as tagged VLAN member under the /interface/bridge/vlan menu for the RSPAN. set switch1 mirror-target=ether3 rspan=yes rspan-egress-vlan-id=999 rspan-ingress-vlan-id=999|
|Sub-menu:|Property Reference||/interface/ethernet/switch||
|Property||||Description|
|ne) no) Sub-menu:|mirror-target (cpu | name | none; Default: no rspan (no | yes; Default: rspan-egress-vlan-id (int eger: 1..4095; Default:) rspan-ingress-vlan-id (int eger: 1..4095; Default:)|1 1|/interface/ethernet/switch/port|Selects a single mirroring target port. Packets from mirror-egress and mirror-ingress (/interface/ethernet /switch/port) and mirror (/interface/ethernet/switch/rule) will be sent to the selected port. Enables Remote Switch Port Analyzer (RSPAN) feature on mirror-target. Traffic marked for ingress or egress mirroring is carried over a specified remote analyzer VLAN-rspan-egress-vlan-id and rspan-ingress-vlan-id. Selects the VLAN ID for marked egress traffic. Only applies when rspan is enabled. Selects the VLAN ID for marked ingress traffic. Only applies when rspan is enabled.|
|Property||||Description|
|Sub-menu:||mirror-egress (no | yes; Default: no) mirror-ingress (no | yes; Default: no)|/interface/ethernet/switch/rule|Whether to send egress packet copy to the mirror-target port. Whether to send ingress packet copy to the mirror-target port.|

Property Description

mirror (no | yes; Default: no) Whether to send a packet copy to mirror-target port.

## <u>Traffic Shaping</u>

It is possible to limit ingress traffic that matches certain parameters with ACL rules and it is possible to limit ingress/egress traffic per port basis. The policer is used for ingress traffic, the shaper is used for egress traffic. The ingress policer controls the received traffic with packet drops. Everything that exceeds the defined limit will get dropped. This can affect the TCP congestion control mechanism on end hosts and achieved bandwidth can be actually less than defined. The egress shaper tries to queue packets that exceed the limit instead of dropping them. Eventually, it will also drop packets when the output queue gets full, however, it should allow utilizing the defined throughput better.

Port-based traffic police and shaper:

/interface ethernet switch port set ether1 ingress-rate=10M egress-rate=5M

MAC-based traffic policer:

/interface ethernet switch rule add ports=ether1 switch=switch1 src-mac-address=64:D1:54:D9:27:E6/FF:FF:FF:FF:FF:FF rate=10M

VLAN-based traffic policer:

/interface bridge set bridge1 vlan-filtering=yes /interface ethernet switch rule add ports=ether1 switch=switch1 vlan-id=11 rate=10M

By enabling vlan-filtering you will be filtering out traffic destined to the CPU, before enabling VLAN filtering you should make sure that you set up a Management port.

Protocol-based traffic policer:

/interface ethernet switch rule add ports=ether1 switch=switch1 mac-protocol=ipx rate=10M

There are other options as well, check the ACL section to find out all possible parameters that can be used to match packets.

The Switch Rule table is used for QoS functionality, see this table on how many rules each device supports.

Due to hardware limitations, the egress-rate and storm-rate settings do not work correctly on 10Gbps switch ports when they are linked at 10/100Mbps, 1/2.5/5Gbps. This applies to 98DX224S, 98DX226S, 98DX2528, 98DX3236 switch chips.

## <u>Traffic Storm Control</u>

Since RouterOS v6.42 it is possible to enable traffic storm control. A traffic storm can emerge when certain frames are continuously flooded on the network. Storm control settings is generally configured on non-uplink ports to restrict incoming storm traffic on those specific ports. This helps safeguard the entire switch and its connected ports by minimizing the impact of traffic storms across the network.

For example, if a network loop has been created and no loop avoidance mechanisms are used (e.g. Spanning Tree Protocol), broadcast or multicast frames can quickly overwhelm the network, causing degraded network performance or even complete network breakdown. Using MikroTik devices with Mar vell Prestera switch it is possible to limit broadcast, unknown multicast and unknown unicast traffic. Unknown unicast traffic is considered when a switch does not contain a host entry for the destined MAC address. Unknown multicast traffic is considered when a switch does not contain a multicast group entry in the /interface bridge mdb menu. Storm control settings should be applied to ingress ports, the egress traffic will be limited.

The storm control parameter is specified in percentage (%) of the link speed. If your link speed is 1Gbps, then specifying storm-rate as 10 will allow only 100Mbps of broadcast, unknown multicast and/or unknown unicast traffic to be forwarded.

Sub-menu: /interface ethernet switch port

|Property||Description|
|---|---|---|
|limit-broadcasts (yes | no; Default: yes)||Limit broadcast traffic on a switch port.|
|limit-unknown-multicasts (yes | no; Default: no)||Limit unknown multicast traffic on a switch port.|
|limit-unknown-unicasts (yes | no; Default: no )||Limit unknown unicast traffic on a switch port.|
|storm-rate (integer 0..100; Default: 100)||Amount of broadcast, unknown multicast and/or unknown unicast traffic is limited to in percentage of the link speed.|

Devices with 8DX224S, 98DX226S, 98DX2528, 98DX3236 switch chip cannot distinguish unknown multicast traffic from all multicast traffic. 9 For example, CRS326-24G-2S+ will limit all multicast traffic when limit-unknown-multicasts and storm-rate is used. For other devices, for example, CRS317-1G-16S+ the limit-unknown-multicasts parameter will limit only unknown multicast traffic (addresses that are not present in /interface bridge mdb).

For example, to limit 1% (10Mbps) of broadcast and unknown unicast traffic on ether1 (1Gbps), use the following commands:

/interface ethernet switch port set ether1 storm-rate=1 limit-broadcasts=yes limit-unknown-unicasts=yes

Due to hardware limitations, the egress-rate and storm-rate settings do not work correctly on 10Gbps switch ports when they are linked at 10/100Mbps, 1/2.5/5Gbps. This applies to 98DX224S, 98DX226S, 98DX2528, 98DX3236 switch chips.

## <u>MPLS hardware offloading</u>

Since RouterOS v6.41 it is possible to offload certain MPLS functions to the switch chip, the switch must be a (P)rovider router in a PE-P-PE setup in order to achieve hardware offloading. A setup example can be found in the Basic MPLS setup example manual page. The hardware offloading will only take place when LDP interfaces are configured as physical switch interfaces (e.g. Ethernet, SFP, SFP+).

Currently only CRS317-1G-16S+ and CRS309-1G-8S+ using RouterOS v6.41 and newer are capable of hardware offloading certain MPLS functions. CRS317-1G-16S+ and CRS309-1G-8S+ built-in switch chip is not capable of popping MPLS labels from packets, in a PE-P-PE setup you either have to use explicit null or disable TTL propagation in MPLS network to achieve hardware offloading.

The MPLS hardware offloading has been removed since RouterOS v7.

## <u>Switch Rules (ACL)</u>

Access Control List contains ingress policy and egress policy engines. See this table on how many rules each device supports. It is an advanced tool for wire-speed packet filtering, forwarding and modifying based on Layer2, Layer3 and Layer4 protocol header field conditions.

ACL rules are checked for each received packet until a match has been found. If there are multiple rules that can match, then only the first rule will be

Enabling features such as IGMP snooping, DHCP snooping, RoMON, PTP, or loop-protect can automatically create dynamic ACL rules. These rules should be considered when adding new ACL entries. Use the place-before property when creating a new rule, or the move command to adjust the ACL

It is not required to set mac-protocol to certain IP version when using L3 or L4 matchers, however, it is recommended to set the mac-

When switch ACL rules are modified (e.g. added, removed, disabled, enabled, or moved), the existing switch rules will be inactive for a short

triggered. A rule without any action parameters is a rule to accept the packet.

rule order.

protocol=ip or mac-protocol=ipv6  when filtering any IP packets.

time. This can cause some packet leakage during the ACL rule modifications.

Sub-menu: /interface ethernet switch rule

Property

copy-to-cpu (no | yes; Default: no)

disabled (yes | no; Default: no)

dscp (0..63)

dst-address (IP address/Mask)

dst-address6 (IPv6 address/Mask)

dst-mac-address (MAC address/Mask)

dst-port (0..65535)

flow-label (0..1048575)

mac-protocol (802.2 | arp | capsman | dot1x | homeplug-av | ip | ipv6 | ipx | lacp | lldp | loop-protect | macsec | mpls-multicast | mpls-unicast | mvrp | packing-compr | packing-simple | pppoe | pppoe-discovery | rarp | romon | service-vlan | vlan | or 0..65535 | or 0x0000-0xffff)

mirror (no | yes)

Description

Clones the matching packet and sends it to the CPU.

Enables or disables ACL entry.

Matching the DSCP field of the packet (only applies to IPv4 packets).

Matching destination IPv4 address and mask. If mac-protocol=arp is specified, matches the destination IP in ARP packets. Without mac- protocol, matches only IPv4 packets.

Matching destination IPv6 address and mask.

Matching destination MAC address and mask.

Matching destination protocol port number (applies to IPv4 and IPv6 packets if mac-protocol is not specified).

Matching IPv6 flow label.

Matching particular MAC protocol specified by protocol name or number

Clones the matching packet and sends it to the mirror-target port.

new-dst-ports (ports | bond | all)

new-vlan-id (0..4095)

new-vlan-priority (0..7)

ports (ports | bond)

protocol (dccp | ddp | egp | encap | etherip | ggp | gre | hmp | icmp | icmpv6 | Matching particular IP protocol specified by protocol name or number. idpr-cmtp | igmp | ipencap | ipip | ipsec-ah | ipsec-esp | ipv6 | ipv6-frag | ipv6-Only applies to IPv4 packets if mac-protocol is not specified. To nonxt | ipv6-opts | ipv6-route | iso-tp4 | l2tp | ospf | pim | pup | rdp | rspf | rsvp | match certain IPv6 protocols, use the mac-protocol=ipv6 setting. sctp | st | tcp | udp | udp-lite | vmtp | vrrp | xns-idp | xtp | or 0..255)

rate (0..4294967295)

redirect-to-cpu (no | yes)

src-address (IP address/Mask)

src-address6 (IPv6 address/Mask)

src-mac-address (MAC address/Mask)

src-port (0..65535)

switch (switch group)

traffic-class (0..255)

vlan-id (0..4095)

vlan-header (not-present | present)

vlan-priority (0..7)

Action parameters:

copy-to-cpu redirect-to-cpu mirror new-dst-ports (can be used to drop packets) new-vlan-id new-vlan-priority rate

Layer2 condition parameters:

dst-mac-address mac-protocol src-mac-address

Changes the destination port to the specified value:

If the setting is left empty (e.g. new-dst-ports=""), the packet will be dropped; If a port or  hardware-offloaded bonding interface is specified, the packet will be redirected to that port. Only single port or bond interface is supported; if you use the all argument, packet will be allowed to pass through to the egress processing without being dropped; If this parameter is not used, the packet will be accepted as is.

Changes the VLAN ID to the specified value. Requires vlan- filtering=yes.

Changes the VLAN priority (priority code point). Requires vlan- filtering=yes.

Matching switch interfaces where the rule will apply to incoming traffic. Multiple ports and hardware-offloaded bonding interfaces can be selected. Note that the switch1-cpu port cannot be selected. If ports property is left empty, the rule will apply to all switch interfaces.

Sets ingress traffic limitation (bits per second) for matched traffic.

Changes the destination port of a matching packet to the CPU.

Matching source IPv4 address and mask. If mac-protocol=arp is specified, matches the source IP in ARP packets. Without mac- protocol, matches only IPv4 packets.

Matching source IPv6 address and mask.

Matching source MAC address and mask.

Matching source protocol port number (applies to IPv4 and IPv6 packets if mac-protocol is not specified).

Matching switch group on which will the rule apply.

Matching IPv6 traffic class.

Matching VLAN ID. Requires vlan-filtering=yes.

Matching VLAN header, whether the VLAN header is present or not. Requires vlan-filtering=yes.

Matching VLAN priority (priority code point).

vlan-id vlan-header vlan-priority

Layer3 condition parameters:

dscp protocol IPv4 conditions: dst-address src-address IPv6 conditions: dst-address6 flow-label src-address6 traffic-class

Layer4 condition parameters:

dst-port src-port

For VLAN related matchers or VLAN related action parameters to work, you need to enable vlan-filtering on the bridge interface and make sure that hardware offloading is enabled on those ports, otherwise, these parameters will not have any effect.

When bridge interface ether-type is set to 0x8100, then VLAN related ACL rules are relevant to frames tagged using regular/customer VLAN 0x8100), this includes vlan-id and new-vlan-id. When bridge interface ether-type is set to 0x88a8, then ACL rules are relevant (TPID to frames tagged with 802.1ad service tag (TPID 0x88a8).

## <u>Port Security</u>

It is possible to limit allowed MAC addresses on a single switch port. For example, to allow 64:D1:54:81:EF:8E MAC address on a switch port, start by switching multiple ports together, in this example 64:D1:54:81:EF:8E is going to be located behind ether1.

Create an ACL rule to allow the given MAC address and drop all other traffic on ether1 (for ingress traffic):

/interface ethernet switch rule add ports=ether1 src-mac-address=64:D1:54:81:EF:8E/FF:FF:FF:FF:FF:FF switch=switch1 add new-dst-ports="" ports=ether1 switch=switch1

Egress traffic can still contain information that should not reach devices with unknown MAC addresses. Assuming the ports are switched, disable MAC learning and disable unknown unicast flooding on ether1:

/interface bridge add name=bridge1 /interface bridge port add bridge=bridge1 interface=ether1 hw=yes learn=no unknown-unicast-flood=no add bridge=bridge1 interface=ether2 hw=yes

With MAC learning disabled, you need to add a static hosts entry for 64:D1:54:81:EF:8E (for egress traffic):

/interface bridge host add bridge=bridge1 interface=ether1 mac-address=64:D1:54:81:EF:8E

Broadcast and multicast traffic will still be sent out from ether1. You can use the broadcast-flood and unknown-multicast-flood param eters to prevent it. Note that some solutions might depend on these settings, such as streaming protocols and DHCP.

## <u>Dual Boot</u>

The “dual boot” feature allows you to choose which operating system you prefer to use on CRS3xx series switches, RouterOS or SwOS. Device operating system could be changed using:

Command-line (/system routerboard settings set boot-os=swos) Winbox Webfig Serial Console

SwOS manual.More details about SwOS are described here:

To check if a model supports booting into SwOS, refer to the SwOS Model table and the product page under Specifications "Operating System".

## <u>Configuring SwOS using RouterOS</u>

Since RouterOS 6.43 it is possible to load, save and reset SwOS configuration, as well as upgrade SwOS and set an IP address for the CRS3xx series switches by using RouterOS.

Save configuration with /system swos save-config

The configuration will be saved on the same device with swos.config as a filename, make sure you download the file from your device since the configuration file will be removed after a reboot.

Load configuration with /system swos load-config Change password with /system swos password Reset configuration with /system swos reset-config Upgrade SwOS from RouterOS using /system swos upgrade

The upgrade command will automatically install the latest available SwOS primary backup version, make sure that your device has access to the Internet in order for the upgrade process to work properly. When the device is booted into SwOS, the version number will include the letter "p", indicating a primary backup version. You can then install the latest available SwOS secondary main version from the SwOS "Upgrade" menu.

Starting from RouterOS version 7.17 device-mode restricts SwOS/RouterOS transition for dual-boot; in order to enable: system/device-mode /update routerboard=yes

Property Description

address-acquisition-mode (d Changes address acquisition method: hcp-only | dhcp-with-fallback dhcp-only-uses only a DHCP client to acquire address | static; Default: dhcp-with- fallback) dhcp-with-fallback-for the first 10 seconds will try to acquire address using a DHCP client. If the request is unsuccessful, then address falls back to static as defined by static-ip-address property

static-address is set as defined by static-ip-address property

allow-from (IP/Mask; Default: IP address or a network from which the switch is accessible. By default, the switch is accessible by any IP address.

0.0.0.0/0) allow-from-ports (name; List of switch ports from which the device is accessible. By default, all ports are allowed to access the switch Default: ) allow-from-vlan (integer: 0.. VLAN ID from which the device is accessible. By default, all VLANs are allowed 4094; Default: )0

identity (name; Default: Mikr Name of the switch (used for Mikrotik Neighbor Discovery protocol) otik)

static-ip-address (IP; Default: IP address of the switch in case address-acquisition-mode is either set to dhcp-with-fallback or static. By setting a static

192.168.88.1) IP address, the address acquisition process does not change, which is DHCP with fallback by default. This means that
the configured static IP address will become active only when there is going to be no DHCP servers in the same broadcast domain

## See also

Basic VLAN switching

Bridge Hardware Offloading

L3HW Route Hardware Offloading

Quality of Service

Spanning Tree Protocol

MTU on RouterBOARD

Layer2 misconfiguration

Bridge VLAN Table

Bridge IGMP/MLD snooping

Multi-chassis Link Aggregation Group
