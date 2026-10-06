---
type: Reference
title: "Neighbor discovery"
description: "Shows the list of protocols the neighbor has been discovered by. The property is available since RouterOS version 7.7."
timestamp: '2026-05-26'
status: active
tags: [routeros, mikrotik, networking]
resource: ~/Downloads/ROS-260526-1445-796.pdf
sources:
  - resource: https://help.mikrotik.com/docs/spaces/ROS/pages/328059/RouterOS
---

# Neighbor discovery

Summary Neighbor list Discovery configuration LLDP

## Summary

Neighbor Discovery protocols allow us to find devices compatible with MNDP (MikroTik Neighbor Discovery Protocol), CDP (Cisco Discovery Protocol), or LLDP (Link Layer Discovery Protocol) in the Layer2 broadcast domain. It can be used to map out your network.

## Neighbor list

The neighbor list shows all discovered neighbors in the Layer2 broadcast domain. It shows to which interface neighbor is connected, its IP/MAC addresses, and other related parameters. The list is read-only, an example of a neighbor list is provided below:

[admin@MikroTik] /ip neighbor print # INTERFACE ADDRESS MAC-ADDRESS IDENTITY VERSION BOARD 0 ether13 192.168.33.2 00:0C:42:00:38:9F MikroTik 5.99 RB1100AHx2 1 ether11 1.1.1.4 00:0C:42:40:94:25 test-host 5.8 RB1000 2 Local 10.0.11.203 00:02:B9:3E:AD:E0 c2611-r1 Cisco I... 3 Local 10.0.11.47 00:0C:42:84:25:BA 11.47-750 5.7 RB750 4 Local 10.0.11.254 00:0C:42:70:04:83 tsys-sw1 5.8 RB750G 5 Local 10.0.11.202 00:17:5A:90:66:08 c7200 Cisco I...

Sub-menu: /ip neighbor

Property

address (IP)

address6 (IPv6)

age (time)

discovered-by (cdp|lldp|mndp)

board (string)

identity (string)

interface (string)

interface-name (string)

ipv6 (yes | no)

mac-address (MAC)

platform (string)

software-id (string)

system-caps (string)

system-caps-enabled (string)

unpack (none|simple|uncompressed- headers|uncompressed-all)

Description

The highest IP address configured on a discovered device

IPv6 address configured on a discovered device

Time interval since last discovery packet

Shows the list of protocols the neighbor has been discovered by. The property is available since RouterOS version 7.7.

RouterBoard model. Displayed only to devices with installed RouterOS

Configured system identity

Interface name to which discovered device is connected

Interface name on the neighbor device connected to the L2 broadcast domain. Applies to CDP.

Shows whether the device has IPv6 enabled.

Mac address of the remote device. Can be used to connect with mac-telnet.

Name of the platform. For example "MikroTik", "cisco", etc.

RouterOS software ID on a remote device. Applies only to devices installed with RouterOS.

System capabilities reported by the Link-Layer Discovery Protocol (LLDP).

Enabled system capabilities reported by the Link-Layer Discovery Protocol (LLDP).

Shows the discovery packet compression type.

uptime (time) Uptime of remote device. Shown only to devices installed with RouterOS.

version (string) Version number of installed software on a remote device

running (string array) Report a list of "features" running on neighbour device. Currently lists only "CAPsMAN" feature.

Starting from RouterOS v6.45, the number of neighbor entries are limited to (total RAM in megabytes)*16 per interface to avoid memory exhaustion.

## Discovery configuration

It is possible to change whether an interface participates in neighbor discovery or not using an Interface list. If the interface is included in the discovery interface list, it will send out basic information about the system and process received discovery packets broadcasted in the Layer2 network. Removing an interface from the interface list will disable both the discovery of neighbors on this interface and also the possibility of discovering this device itself on that interface.

/ip neighbor discovery-settings

Property Description

discover-Interface list on which members the discovery protocol will run on. interface-list (stri ng; Default: static )

discover-interval Adjusts the frequency at which neighbor discovery packets are transmitted. It also adjusts the Time-to-Live (TTL) TLV value for CDP (time: 5s.. and LLDP packets using the formula: (discover-interval * 4) + 1. The setting is available since RouterOS version 7.16. 9h6m8s; Default: 30s)

lldp-dcbx (yes | Whether to send Data Center Bridging Capabilities Exchange Protocol (DCBX) TLVs, which allows to communicate switch QoS no; Default: no) settings and capabilities with other neighboring devices using LLDP. Only applies to MikroTik devices with Marvell Prestera switch (e.

g. CRS3xx). Enabled DCBX includes the following TLVs:
1. ETS (Enhanced Transmission Selection) Configuration TLV. This TLV is used to share the switch's ETS configuration. It includes:
a. The willingness bit, which indicates whether the device is willing to accept QoS configuration from neighboring devices. In RouterOS, the willing bit is set to disabled, meaning the switch will not accept remote configurations and instead uses its own settings.
b. The priority assignment table, which maps priorities to specific traffic-class.
c. The bandwidth allocation table, where RouterOS calculates the percentage of bandwidth allocated to each queue based on the weight property. This applies to queues using the high-priority-group in the /interface/ethernet /switch/qos/tx-manager/queue settings.
d. The Transmission Selection Algorithm (TSA) table, where high-priority-group queues are assigned to ETS, strict -priority queues to Strict Priority, and low-priority-group or non-hardware offloaded queues to the Vendor Specific Algorithm.
2. ETS Recommendation TLV. This provides a recommendation on how neighboring devices should configure ETS. RouterOS uses the same data as in the ETS Configuration TLV to give its recommendation.
3. Priority-based Flow Control Configuration TLV. This TLV is used to share PFC configuration. Similar to the ETS TLV, the willingness bit is set to disabled, meaning the switch does not accept remote PFC configurations. PFC is enabled for specific priorities based on settings configured under /interface/ethernet/switch/qos/priority-flow-control, and /inte rface/ethernet/switch/qos/port.
4. Application Priority TLV. This TLV is used to communicate how different applications are prioritized in the network.
5. Application VLAN TLV. This TLV is used to share VLAN configurations for applications. RouterOS currently does not support sending values in this TLV and will send an empty VLAN table instead.

lldp-mac-phy- config (yes | no; Default: no)

lldp-max-frame- size (yes | no; Default: no)

lldp-med (yes | no; Default: yes)

lldp-poe-power ( yes | no; Default: yes)

Whether to send MAC/PHY Configuration/Status TLV in LLDP, which indicates the interface capabilities, current setting of the duplex status, bit rate, and auto-negotiation. Only applies to the Ethernet interfaces. While TLV is optional in LLDP, it is mandatory when sending LLDP-MED, meaning this TLV will be included when necessary even though the property is configured as disabled.

Whether to send Maximum Frame Size TLV in LLDP, which indicates the maximum frame size capability of the interface in bytes (l2 mtu + 18). Only applies to the Ethernet interfaces.

Specifies whether to advertise the LLDP-MED Media Capabilities TLV. This option must be enabled when lldp-med-net- policy-vlan is used. The setting is available since RouterOS version 7.23.

Two specific TLVs facilitate Power over Ethernet (PoE) management between Power Sourcing Equipment (PSE) and Powered Devices (PD):

IEEE 802.3 Organizationally Specific Power Via MDI TLV TIA-1057 (LLDP-MED) Organizationally Specific Extended Power via MDI TLV

The lldp-poe-power attribute determines whether to transmit the IEEE 802.3 Organizationally Specific Power Via MDI TLV in LLDP messages.

The transmission of LLDP-MED Organizationally Specific Extended Power via MDI TLV is not configurable. It is automatically included in outgoing LLDP-MED packets when the remote device has transmitted LLDP-MED capability of receiving power.

These TLVs are relevant only for Ethernet interfaces that support PoE-Out. The setting is available since RouterOS version 7.15, and it replaces PoE-out port poe-lldp-enabled setting.

Advertised VLAN ID for LLDP-MED Network Policy TLV. This allows assigning a VLAN ID for LLDP-MED capable devices, such as VoIP phones. The TLV will only be added to interfaces where LLDP-MED capable devices are discovered and lldp-med is enabled. Other TLV values are predefined and cannot be changed:

Application Type-Voice VLAN Type-Tagged L2 Priority - 0 DSCP Priority - 0

When used together with the bridge interface, the (R/M)STP protocol should be enabled with protocol-mode setting.

Additionally, other neighbor discovery protocols (e.g. CDP) should be excluded using protocol setting to avoid LLDP-MED misconfiguration.

Whether to send IEEE 802.1 Organizationally Specific TLVs in LLDP related to VLANs.

When this setting is enabled, three TLVs are advertised:

Port VLAN ID. This applies to the bridge port's pvid property. Port And Protocol VLAN ID. This TLV is not used and always indicates "not supported" and "not enabled". VLAN Name. This includes up to 10 active VLANs from the "/interface/bridge/vlan" table.

These TLVs are relevant to interfaces that are added to a vlan-filtering bridge, and the setting is available since RouterOS version

7.16. Selects the neighbor discovery packet sending and receiving mode. The setting is available since RouterOS version 7.7.
lldp-med-net- policy-vlan (integ er 0..4094;

lldp-vlan-info (ye s | no; Default: no )

mode (rx-only | tx-only | tx-and- rx; Default: tx- and-rx)

protocol (cdp | lldp | mndp; Default: cdp,lldp, mndp)

List of used discovery protocols.

Default: disabled)

Since RouterOS v6.44, neighbor discovery is working on individual slave interfaces. Whenever a master interface (e.g. bonding or bridge) is included in the discovery interface list, all its slave interfaces will automatically participate in neighbor discovery. It is possible to allow neighbor discovery only to some slave interfaces. To do that, include the particular slave interface in the list and make sure that the master interface is not included.

/interface bonding add name=bond1 slaves=ether5,ether6 /interface list add name=only-ether5 /interface list member add interface=ether5 list=only-ether5 /ip neighbor discovery-settings set discover-interface-list=only-ether5

Now the neighbor list shows a master interface and actual slave interface on which a discovery message was received.

[admin@R2] > ip neighbor print # INTERFACE ADDRESS MAC-ADDRESS IDENTITY VERSION BOARD 0 ether5 192.168.88.1 CC:2D:E0:11:22:33 R1 6.45.4 ... CCR1036- 8G-2S+ bond1

## LLDP

Depending on RouterOS configuration, different type-length-value (TLV) can be sent in the LLDP message, this includes:

Chassis ID (MAC address) Port ID (interface name) Time To Live System Name (system identity) System Description (platform-MikroTik, software version-RouterOS version,  hardware name-RouterBoard name) Management Address (all IP addresses configured on the port) System Capabilities (enabled system capabilities, e.g. bridge or router) Port Description (combined interface name like "bridge/ether1" if the sending interface is part of bridge or bond, or interface name same as Port ID) IEEE 802.1 Port VLAN ID IEEE 802.1 Port And Protocol VLAN ID IEEE 802.1 VLAN Name IEEE 802.3 MAC/PHY Configuration/Status IEEE 802.3 Power Via MDI IEEE 802.3 Maximum Frame Size LLDP-MED Media Capabilities (list of MED capabilities) LLDP-MED Network Policy (assigned VLAN ID for voice traffic) LLDP-MED Extended Power via MDI Port Extension (Port Extender and Controller Bridge advertisement) End of LLDPDU
