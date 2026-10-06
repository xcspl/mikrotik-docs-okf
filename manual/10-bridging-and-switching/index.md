# Bridging and Switching

* [Bridging and Switching](bridging-and-switching.md) - Ethernet-like networks (Ethernet, Ethernet over IP, IEEE 802.11 in ap-bridge or bridge mode, WDS, VLAN) can be connected together using MAC bridges. The bridge feature allows the interconnection of hosts connected to
* [Marvell Prestera switch chip features](marvell-prestera-switch-chip-features.md) - MikroTik devices with Marvell Prestera switch chip offer high-performance Layer 2 and Layer 3 features including advanced forwarding, routing offloading, VLAN support, QoS, mirroring, and PTP synchronization for
* [L3 Hardware Offloading](l3-hardware-offloading.md) - L3 Hardware Offloading enables routing at wire speed by offloading CPU-intensive tasks to the switch chip. This page details how to configure L3HW for entire switches, individual ports, and global settings like IPv6
* [Quality of Service](quality-of-service.md) - This documentation introduces Quality of Service (QoS) features in MikroTik RouterOS for devices with Marvell Prestera switch chips, detailing QoS prioritization, traffic shaping, and congestion management. It covers
* [MACsec](macsec.md) - MACsec is a security protocol for Ethernet networks providing confidentiality, integrity, and authenticity using GCM-AES-128 encryption. RouterOS supports MACsec with manual key configuration and limited hardware
* [MACVLAN](macvlan.md) - MACVLAN allows creating multiple virtual network interfaces with unique MAC addresses on a physical interface, enabling efficient IP address management and distinct PPPoE connections. It operates at the MAC level
* [VXLAN](vxlan.md) - This page documents MikroTik RouterOS's VXLAN implementation, covering its purpose in expanding VLAN IDs, configuration options for VXLAN interfaces and VTEPs, and forwarding table monitoring. It details settings
* [Switch Chip Features](switch-chip-features.md) - This page introduces MikroTik RouterOS switch chip features, detailing supported functionalities like Port Switching and Mirroring across various models, along with limitations in bandwidth controls and VLAN
* [VLAN](vlan.md) - This page introduces VLAN functionality in MikroTik RouterOS, explaining how to create and manage Virtual LANs using IEEE 802.1Q standards for efficient network segmentation, with details on VLAN interfaces,

## SwOS

* [SwOS](swos.md) - SwOS is a lightweight operating system built exclusively for the administration of MikroTik switching hardware. It delivers maximum wire-speed Layer 2 forwarding capability across all standard Ethernet frames,
* [CRS3xx and CSS3xx Series Manual](crs3xx-and-css3xx-series-manual.md) - SwOS is an operating system designed specifically for the administration of MikroTik switch products. It provides fundamental managed switch functionalities alongside advanced features such as port-to-port
* [CSS106 (RB260) series Manual](css106-rb260-series-manual.md) - SwOS configuration manual for the MikroTik CSS106 (RB260) series switch: port and link settings, VLANs, SFP, statistics, and system management
* [CSS610 series Manual](css610-series-manual.md) - SwOS Lite is an operating system designed specifically for the administration of MikroTik CSS610 series switch products. CSS610 series switches support only SwOS Lite operating system
* [GPEN21 series Manual](gpen21-series-manual.md) - SwOS Lite manual for the MikroTik GPEN21 smart PoE power injector and repeater: features, port settings, VLANs, and switch management
* [Cannot upgrade SwOS](cannot-upgrade-swos.md) - MikroTik switches that support SwOS store two separate firmware images in flash memory: a primary (active) image and a backup image. Under normal operation, the device boots from the primary image. When a firmware

## User Guides

* [Bridging and Switching Case Studies](bridging-and-switching-case-studies.md) - This page presents practical case studies for RouterOS bridging and switching, covering VLAN configurations, IGMP/MLD snooping, spanning tree protocols, loop prevention, and switch-chip behavior to aid Layer 2
* [Basic VLAN switching](basic-vlan-switching.md) - This page provides an overview of basic VLAN switching configuration on MikroTik RouterOS, covering setup for devices with Marvell Prestera and RTL8367/CRS series switch chips, including hardware-offloaded VLAN
* [Bridge IGMP/MLD snooping](bridge-igmpmld-snooping.md) - This page documents MikroTik RouterOS bridge features for IGMP/MLD snooping, enabling efficient multicast traffic forwarding by filtering streams to subscribed ports. It covers configuration options for IGMP/MLD
* [Bridge VLAN Table](bridge-vlan-table.md) - This page introduces MikroTik RouterOS's Bridge VLAN Table feature, explaining how to configure VLAN filtering in bridges using tagged/untagged ports, PVIDs, and ingress/egress rules. It includes setup examples for
* [CRS1xx/2xx series switch examples](crs1xx2xx-series-switch-examples.md) - This page provides configuration examples and use cases for Cloud Router Switch features on CRS1xx/2xx series switches, covering port switching, management access setup with VLAN filtering, and security
* [Layer2 misconfiguration](layer2-misconfiguration.md) - This page addresses Layer2 misconfigurations in MikroTik RouterOS, focusing on issues like improper bridge setups with hardware offloading and port isolation. It explains symptoms such as low throughput, high CPU
* [Loop Protect](loop-protect.md) - Loop Protect prevents Layer2 loops by detecting and disabling interfaces receiving their own loop-protect packets, with configurable intervals and disable times. It supports Ethernet, VLAN, EoIP, and VxLAN
* [Spanning Tree Protocol](spanning-tree-protocol.md) - This page explains the Spanning Tree Protocol (STP) in MikroTik RouterOS, detailing how it prevents network loops by selecting a root bridge and optimizing port usage through Bridge Protocol Data Units (BPDUs). It
* [Wireless VLAN Trunk](wireless-vlan-trunk.md) - This page explains how to configure Wireless VLAN Trunking on MikroTik RouterOS using bridge VLAN filtering, allowing selective forwarding of specific VLANs over a wireless PtP link while blocking others. It covers
* [WMM and VLAN priority](wmm-and-vlan-priority.md) - This page explains how MikroTik RouterOS implements WMM (Wi-Fi MultiMedia) and VLAN priority for QoS, detailing how traffic is categorized into access categories (background, best effort, video, voice), VLAN priority
