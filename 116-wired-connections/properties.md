---
type: Reference
title: "Properties"
description: "This section describes the Ethernet interface configuration options."
timestamp: '2026-05-26'
status: active
tags: [routeros, mikrotik, networking]
resource: ~/Downloads/ROS-260526-1445-796.pdf
sources:
  - resource: https://manual.mikrotik.com/docs/introduction/
---

# Properties

Sub-menu: /interface ethernet

This section describes the Ethernet interface configuration options.

Property

advertise (since RouterOS v7.12: 10M-baseT-half | 10M-baseT-full| 100M-baseT-half | 100M-baseT-full | 1G-baseT-half | 1G-baseT-full | 1G-baseX | 2.5G-baseT | 2.5G-baseX | 5G-baseT | 10G-baseT | 10G-baseSR-LR | 10G-baseCR | 40G-baseSR4-LR4 | 40G- baseCR4 | 25G-baseSR-LR | 25G-baseCR | 50G-baseSR2-LR2 | 50G-baseCR2 | 100G-baseSR4-LR4 | 100G-baseCR4; Default: )

(older RouterOS: 10M-full | 10M-half | 100M-full | 100M-half | 1000M- full | 1000M-half | 2500M-full | 5000M-full | 10000M-full; Default: )

arp (disabled | enabled | local-proxy-arp | proxy-arp | reply-only; Default: enabled) Address Resolution Protocol mode:

disabled-the interface will not use ARP enabled-the interface will use ARP local-proxy-arp-the router performs proxy ARP on the interface and sends replies to the same interface proxy-arp-the router performs proxy ARP on the interface and sends replies to other interfaces reply-only-the interface will only reply to requests originated from matching IP address/MAC address combinations which are entered as static entries in the ARP table. No dynamic entries will be automatically stored in the ARP table. Therefore for communications to be successful, a valid static entry must already exist.

How long the ARP record is kept in the ARP table after no packets are received from IP. Value auto equals to the value of arp-timeout in IP /Settings, default is 30s.

arp-timeout (auto | integer; Default: auto)

auto-negotiation (yes | no; Default: yes) When enabled, the interface "advertises" its maximum capabilities to achieve the best connection possible.

Note1: Auto-negotiation should not be disabled on one end only, otherwise Ethernet Interfaces may not work properly. Note2: Gigabit Ethernet and NBASE-T Ethernet links cannot work with auto-negotiation disabled.

bandwidth (integer/integer; Default: unlimited/unlimited) Sets max rx/tx bandwidth in kbps that will be handled by an interface. TX limit is supported on all Atheros switch-chip ports. RX limit is supported only on Atheros8327/QCA8337 switch-chip ports.

cable-setting (default | short | standard; Default: default) Changes the cable length setting (only applicable to NS DP83815/6 cards)

combo-mode (auto | copper | sfp; Default: auto) When auto mode is selected, the port that was first connected will establish the link. In case this link fails, the other port will try to establish a new link. In case of a reboot, any of the two ports can be running, it depends on which port will successfully establish the link first. When sfp mode is selected, the interface will only work through SFP/SFP+ cage. When copper mode is selected, the interface will only work through RJ45 Ethernet port.

comment (string; Default: ) Descriptive name of an item

disable-running-check (yes | no; Default: yes) Disable running check. If this value is set to 'no', the router automatically detects whether the NIC is connected with a device in the network or not. Default value is 'yes' because older NICs do not support it. (relevant only to CHR and x86)

fec-mode (auto | fec74 | fec91 | off; Default: auto) Changes Forward Error Correction (FEC) mode for SFP28, QSFP+ and QSFP28 interfaces. Same mode should be used on both link ends, otherwise FEC mismatch could result in non-working link or even false link-ups.

It is recommended to enable FEC, particularly when creating link between CRS3xx, CRS5xx series switches. Some optical modules might rely on FEC functionality in MACs.

auto-same as off fec74 - enables IEEE 802.3 clause 74 FEC (aka FC-FEC), can be used with 25Gbps, 40Gbps and 50Gbps link modes fec91 - enables IEEE 802.3 clause 91 FEC (aka RS-FEC), can be used with 25Gbps, 50Gbps, 100Gbps, 200Gbps and 400Gbps link modes off-disabled FEC.

tx-flow-control (on | off | auto; Default: off) When set to on, the port will generate pause frames to the upstream device to temporarily stop the packet transmission. Pause frames are only generated when some routers output interface is congested and packets cannot be transmitted anymore. auto is the same as on except when auto- negotiation=yes flow control status is resolved by taking into account what other end advertises.

rx-flow-control (on | off | auto; Default: off) When set to on, the port will process received pause frames and suspend transmission if required. auto is the same as on except when auto- negotiation=yes flow control status is resolved by taking into account what other end advertises.

full-duplex (yes | no; Default: yes) Defines whether the transmission of data appears in two directions simultaneously, only applies when auto-negotiation is disabled. Since RouterOS v7.12, the setting is replaced with new speed link modes.

l2mtu (integer [0..65536]; Default: ) Layer2 Maximum transmission unit. Read more.

mac-address (MAC; Default: ) Media Access Control number of an interface.

mdix-enable (yes | no; Default: yes) Whether the MDI/X auto cross over cable correction feature is enabled for the port (Hardware specific, e.g. ether1 on RB500 can be set to yes/no. Fixed to 'yes' on other hardware.)

mtu (integer [0..65536]; Default: 1500)

name (string; Default: )

orig-mac-address (read-only: MAC; Default: )

passthrough-interface (interface; Default: )

poe-out (auto-on | forced-on | off; Default: off)

poe-priority (integer [0..99]; Default: )

sfp-shutdown-temperature (integer; Default: 95 | 80)

sfp-rate-select (high | low; Default: high)

speed (since RouterOS v7.12: 10M-baseT-half | 10M-baseT-full| 100M-baseT-half | 100M-baseT-full | 1G-baseT-half | 1G-baseT-full | 1G-baseX | 2.5G-baseT | 2.5G-baseX | 5G-baseT | 10G-baseT | 10G-baseSR-LR | 10G-baseCR | 40G-baseSR4-LR4 | 40G- baseCR4 | 25G-baseSR-LR | 25G-baseCR | 50G-baseSR2-LR2 | 50G-baseCR2 | 100G-baseSR4-LR4 | 100G-baseCR4; Default: )

(older RouterOS: 10Mbps | 10Gbps | 100Mbps | 1Gbps | 2.5Gbps | 5Gbps | 25Gbps | 40Gbps | 100Gbps; Default: )

Read-only properties

Property Description

Layer3 Maximum transmission unit

Name of an interface

Original Media Access Control number of an interface.

Sets an interface in passthrough mode on CCR2004-1G-2XS-PCIe device. By default, the PCIe interface will show up as four virtual Ethernet interfaces. Two interfaces in passthrough mode to the 25G SFP28 cages. The remaining two virtual Ethernet-PCIe interfaces are bridged with the Gigabit Ethernet port for management access.

Poe Out settings. Read more.

Poe Out settings. Read more.

The temperature in Celsius at which the interface will be temporarily turned off due to too high detected SFP module temperature (introduced v6.48). The default value for SFP/SFP+/SFP28 interfaces is 95, and for QSFP+ /QSFP28 interfaces 80 (introduced v7.6).

Allows to control rate select pin for SFP ports.

Sets interface data transmission speed which takes effect only when auto- negotiation is disabled. Setting higher speeds than the actual interface supported speed can result in undefined behavior. Single option is allowed.

switch (integer) ID to which switch chip interface belongs to.

## Menu specific commands

Property Description

blink ([id, name]) Blink Ethernet leds

monitor ([id, name])

reset-counters ([id, name])

reset-mac-address ([id, name])

cable-test (string)

## Monitor

different transceivers (e.g. SFP and QSFP).

Properties

running (yes | no) Whether interface is running. Note that some interface does not have running check and they are always reported as "running".

slave (yes | no) Whether interface is configured as a slave of another interface (for example Bonding or Bridge)

Monitor ethernet status. Read more.

Reset stats counters. Read more.

Reset MAC address to manufacturers default.

Shows detected problems with cable pairs. Read More.

To print out a current link rate and other Ethernet related properties or to see detailed diagnostics information for transceivers, use "/interface ethernet monitor" command. The provided information can differ for different interface types (e.g. Ethernet over twisted pair or SFP interface) or for

Property Description

advertising (since RouterOS v7.12: 10M-baseT-half | 10M-baseT-full| 100M-baseT-half | 100M-baseT-full | 1G-baseT-half | Advertised link 1G-baseT-full | 1G-baseX | 2.5G-baseT | 2.5G-baseX | 5G-baseT | 10G-baseT | 10G-baseSR-LR | 10G-baseCR | 40G-modes, only applies baseSR4-LR4 | 40G-baseCR4 | 25G-baseSR-LR | 25G-baseCR | 50G-baseSR2-LR2 | 50G-baseCR2 | 100G-baseSR4-LR4 | when auto- 100G-baseCR4) negotiation is enabled (older RouterOS: 10M-full | 10M-half | 100M-full | 100M-half | 1000M-full | 1000M-half | 2500M-full | 5000M-full | 10000M-full)

auto-negotiation (disabled | done | failed | incomplete) Current auto- negotiation status:

disabled-negotiation disabled done-negotiation completed failed-negotiation failed incomplete-negotiation not completed yet

default-cable-settings (short | standard) Default cable length setting (only applicable to NS DP83815/6 cards)

short-support short cables standard-support standard cables

fec (fec74 | fec91 | off) Current FEC mode.

full-duplex (yes | no) Whether transmission of data occurs in two directions simultaneously

link-partner-advertising (since RouterOS v7.12: 10M-baseT-half | 10M-baseT-full| 100M-baseT-half | 100M-baseT-full | 1G-Link partner baseT-half | 1G-baseT-full | 1G-baseX | 2.5G-baseT | 2.5G-baseX | 5G-baseT | 10G-baseT | 10G-baseSR-LR | 10G-baseCR advertised link | 40G-baseSR4-LR4 | 40G-baseCR4 | 25G-baseSR-LR | 25G-baseCR | 50G-baseSR2-LR2 | 50G-baseCR2 | 100G-modes, only applies baseSR4-LR4 | 100G-baseCR4) when auto- negotiation is (older RouterOS: 10M-full | 10M-half | 100M-full | 100M-half | 1000M-full | 1000M-half | 2500M-full | 5000M-full | 10000M-full) enabled

rate (10Mbps | 100Mbps | 1Gbps | 2.5Gbps | 5Gbps | 10Gbps | 25Gbps | 40Gbps | 50Gbps | 100Gbps | 200Gbps | 400Gbps) Actual data rate of the connection.

status (link-ok | no-link | unknown) Current link status of an interface

link-ok-the card is connected to the network no-link-the card is not connected to the network unknown-the connection is not recognized (if the card does not report connection status)

tx-flow-control (yes | no) Whether TX flow control is used

rx-flow-control (yes | no) Whether RX flow control is used

combo-state (copper | sfp) Used combo-mode for combo interfaces

sfp-module-present (yes | no) Whether a transceiver is in cage

sfp-rx-lose (yes | no) Whether a receiver signal is lost

sfp-tx-fault (yes | no) Whether a transceiver transmitter is in fault state

sfp-type (SFP/SFP+/SFP28/SFP56 | DWDM-SFP/SFP+ | QSFP | QSFP+ | QSFP28/QSFP56 | QSFPDD) Used transceiver type

sfp-cmis-revision (string) Transceiver CMIS revision number

sfp-connector-type (SC | LC | optical-pigtail | copper-pigtail | multifiber-parallel-optic-1x12 | multifiber-parallel-optic-1x16 | no-Used transceiver separable-connector | RJ45) connector type

sfp-link-length-9um ( ) m Transceiver supported link length for single mode 9 /125um fiber

sfp-link-length-sm (km) Transceiver supported link length for single mode fiber

sfp-link-length-om3 (m) Transceiver supported link length for multi mode (OM3)

sfp-link-length-om4 (m) Transceiver supported link length for multi mode (OM4)

sfp-link-length-om5 (m)

sfp-link-length-50um (m)

sfp-link-length-62um (m)

sfp-link-length-copper (m)

sfp-vendor-name (string)

sfp-vendor-part-number (string)

sfp-vendor-revision (string)

sfp-vendor-serial (string)

sfp-manufacturing-date (date)

sfp-power-class (string)

sfp-max-power (W)

sfp-wavelength (nm)

sfp-temperature (C)

sfp-supply-voltage (V)

sfp-tx-bias-current (mA)

sfp-tx-power (dBm)

sfp-rx-power (dBm)

baseSR8-LR8 | 400G-baseCR8)

Transceiver supported link length for multi mode (OM5)

Transceiver supported link length for multi mode 50 /125um fiber (OM2)

Transceiver supported link length for multi mode 62.5 /125um fiber (OM1)

Supported link length of copper transceiver

Transceiver manufacturer

Transceiver part number

Transceiver revision number

Transceiver serial number

Transceiver manufacturing date

Transceiver power class

Transceiver maximum power consumption

Transceiver transmitter optical signal wavelength

Transceiver temperature

Transceiver supply voltage

Transceiver Tx bias current

Transceiver transmitted optical power

Transceiver received optical power

sfp-supported (10M-baseT-half | 10M-baseT-full| 100M-baseT-half | 100M-baseT-full | 1G-baseT-half | 1G-baseT-full | 1G-Module supported baseX | 2.5G-baseT | 2.5G-baseX | 5G-baseT | 10G-baseT | 10G-baseSR-LR | 10G-baseCR | 40G-baseSR4-LR4 | 40G-link modes. This baseCR4 | 25G-baseSR-LR | 25G-baseCR | 50G-baseSR2-LR2 | 50G-baseCR2 | 100G-baseSR4-LR4 | 100G-baseCR4 | property only applies 50G-baseSR-LR | 50G-baseCR | 100G-baseSR2-LR2 | 100G-baseCR2 | 200G-baseSR4-LR4 | 200G-baseCR4 | 400G-to certain devices.

supported (10M-baseT-half | 10M-baseT-full| 100M-baseT-half | 100M-baseT-full | 1G-baseT-half | 1G-baseT-full | 1G-baseX Shows the | 2.5G-baseT | 2.5G-baseX | 5G-baseT | 10G-baseT | 10G-baseSR-LR | 10G-baseCR | 40G-baseSR4-LR4 | 40G-baseCR4 | supported interface 25G-baseSR-LR | 25G-baseCR | 50G-baseSR2-LR2 | 50G-baseCR2 | 100G-baseSR4-LR4 | 100G-baseCR4 | 50G-baseSR-hardware link mode LR | 50G-baseCR | 100G-baseSR2-LR2 | 100G-baseCR2 | 200G-baseSR4-LR4 | 200G-baseCR4 | 400G-baseSR8-LR8 | capabilities. 400G-baseCR8)

eeprom-checksum (good | bad) Whether EEPROM checksum is correct

eeprom (hex dump) Raw EEPROM of the transceiver

Example output of an Ethernet status:

[admin@MikroTik] > /interface ethernet monitor ether2 name: ether2 status: link-ok auto-negotiation: done rate: 1Gbps full-duplex: yes tx-flow-control: no rx-flow-control: no supported: 10M-baseT-half,10M-baseT-full,100M-baseT-half,100M-baseT-full,1G-baseT-half,1G- baseT-full advertising: 10M-baseT-half,10M-baseT-full,100M-baseT-half,100M-baseT-full,1G-baseT-half,1G- baseT-full link-partner-advertising: 10M-baseT-half,10M-baseT-full,100M-baseT-half,100M-baseT-full,1G-baseT-half,1G- baseT-full

Example output of an SFP status:

[admin@MikroTik] > /interface ethernet monitor sfp3 name: sfp3 status: link-ok auto-negotiation: done rate: 1Gbps full-duplex: no tx-flow-control: no rx-flow-control: no supported: 10M-baseT-half,10M-baseT-full,100M-baseT-half,100M-baseT-full,1G-baseT-half,1G- baseT-full,1G-baseX sfp-supported: 1G-baseX advertising: 1G-baseX link-partner-advertising: sfp-module-present: yes sfp-rx-loss: no sfp-tx-fault: no sfp-type: SFP/SFP+/SFP28/SFP56 sfp-connector-type: LC sfp-link-length-om1: 500m sfp-link-length-om2: 550m sfp-vendor-name: Mikrotik sfp-vendor-part-number: S-85DLC05D sfp-vendor-serial: SG85M31401687 sfp-manufacturing-date: 13-04-24 sfp-wavelength: 850nm sfp-temperature: 33C sfp-supply-voltage: 3.237V sfp-tx-bias-current: 2mA sfp-tx-power: -5.792dBm sfp-rx-power: -5.22dBm eeprom-checksum: good
eeprom: 0000: 03 04 07 00 00 00 01 00 00 00 00 03 0d 00 00 00 ........ ........
0010: 37 32 00 00 4d 69 6b 72 6f 74 69 6b 20 20 20 20 72..Mikr otik
0020: 20 20 20 20 00 00 00 00 53 2d 38 35 44 4c 43 30 .... S-85DLC0
0030: 35 44 20 20 20 20 20 20 00 00 00 00 03 52 00 50 5D .....R.P
0040: 00 1a 00 00 53 47 38 35 4d 33 31 34 30 31 36 38 ....SG85 M3140168
0050: 37 20 20 20 31 33 30 34 32 34 20 20 68 b0 01 f3 7 1304 24 h...
0060: 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 ........ ........
*
0080: 64 00 d2 ff 5a 00 d7 ff 8c a0 75 30 88 b8 79 18 d...Z... ..u0..y.
0090: 75 30 00 fa 61 a8 01 f4 1f 07 03 1a 18 a5 03 e7 u0..a... ........
00a0: 31 2e 00 13 27 12 00 27 00 00 00 00 00 00 00 00 1...'..' ........
00b0: 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 ........ ........
00c0: 00 00 00 00 3f 80 00 00 00 00 00 00 01 00 00 00 ....?... ........
00d0: 01 00 00 00 01 00 00 00 01 00 00 00 00 00 00 23 ........ .......#
00e0: 21 7c 7e 72 05 27 0a 4b 0b be 00 00 00 00 00 94 !|~r.'.K ........
00f0: 00 00 00 00 00 00 00 00 20 21 2a ff ff ff ff 00 ........ !*.....

## Detect Cable Problems

A cable test can detect problems or measure the approximate cable length if the cable is unplugged on the other end and there is, therefore, "no-link". RouterOS will show:

which cable pair is damaged the distance to the problem how exactly the cable is broken-short-circuited or open-circuited

This also works if the other end is simply unplugged-in that case, the total cable length will be shown.

Here is an example output:

[admin@CCR] > interface ethernet cable-test ether2 name: ether2 status: no-link cable-pairs: open:4,open:4,open:4,open:4

In the above example, the cable is not shorted but “open” at 4 meters distance, all cable pairs are equally faulty at the same distance from the switch chip.

Currently cable-test is implemented on the following devices:

||Devices||
|---|---|---|
|CCR1xxx series|RB952Ui-5ac2nD|RBLHGG-5acD|
|CRS1xx series|RB962UiGS-5HacT2HnT|RB5009 series (eth1)|
|CRS2xx series|RB1100AHx2|C52iG-5HaxD2HaxD|
|OmniTIK series|RB1100x4|C53UiG+5HPaxD2HPaxD|
|RB450G series|RBD52G-5HacD2HnD|S53UG+5HaxD2HaxD series|
|RB951 series|RBD53G-5HacD2HnD series|H53UiG-5HaxQ2HaxQ|
|RB2011 series|RBcAPGi-5acD2nD||
|RB4011 series|RBmAPL-2nD||
|RB750Gr2|RBmAP2nD||
|RB750UPr2|RBwsAP-5Hac2nD||
|RB751U-2HnD|RB3011UiAS-RM||
|RB850Gx2|RBMetal 2SHPn||
|RB931-2nD|RBDynaDishG-5HacD||
|RB941-2nD|RBLDFG-5acD||

Currently cable-test is not supported on Combo ports.

## Stats

Using "/interface ethernet print stats" command, it is possible to see a wide range of Ethernet-related statistics. The list of statistics can differ between RouterBoard devices due to different Ethernet drivers. The list below contains all available counters across all RouterBoard devices. Most of the Ethernet statistics can be remotely monitored using SNMP and MIKROTIK-MIB.

Property Description

driver-rx-byte (integer) Total count of received bytes on device CPU

driver-rx-packet (integer) Total count of received packets on device CPU

driver-tx-byte (integer) Total count of transmitted bytes by device CPU

driver-tx-packet (integer) Total count of transmitted packets by device CPU

fc-fec-block-corrected (integer) Total count of FC-FEC corrected blocks. Applies only when fec74 mode is used.

fc-fec-block-uncorrected (integ Total count of FC-FEC uncorrected blocks. Applies only when fec74 mode is used. er)

fc-fec-rx-block (integer) Total count of FC-FEC received blocks. Applies only when fec74 mode is used.

rs-fec-corrected (integer) Total count of RS-FEC corrected codewords. Applies only when fec91 mode is used.

rs-fec-symbol-error (integer) Total count of RS-FEC symbol errors. Applies only when fec91 mode is used.

rs-fec-uncorrected (integer)

rx-64 (integer)

rx-65-127 (integer)

rx-128-255 (integer)

rx-256-511 (integer)

rx-512-1023 (integer)

rx-1024-1518 (integer)

rx-1519-max (integer)

rx-align-error (integer)

rx-broadcast (integer)

rx-bytes (integer)

rx-carrier-error (integer)

rx-code-error (integer)

rx-control (integer)

rx-error-events (integer)

rx-fcs-error (integer)

rx-fragment (integer)

rx-ip-header-checksum-error (i nteger)

rx-jabber (integer)

rx-length-error (integer)

rx-multicast (integer)

rx-overflow (integer)

rx-pause (integer)

rx-runt (integer)

rx-tcp-checksum-error (integer)

rx-too-long (integer)

rx-too-short (integer)

rx-udp-checksum-error (integer)

rx-unicast (integer)

rx-unknown-op (integer)

tx-64 (integer)

tx-65-127 (integer)

tx-128-255 (integer)

tx-256-511 (integer)

tx-512-1023 (integer)

Total count of RS-FEC uncorrected codewords. Applies only when fec91 mode is used.

Total count of received 64 byte frames

Total count of received 65 to 127 byte frames

Total count of received 128 to 255 byte frames

Total count of received 256 to 511 byte frames

Total count of received 512 to 1023 byte frames

Total count of received 1024 to 1518 byte frames

Total count of received frames larger than 1519 bytes

Total count of received align error events-packets where bits are not aligned along octet boundaries

Total count of received broadcast frames

Total count of received bytes

Total count of received frames with carrier sense error

Total count of received frames with code error

Total count of received control or pause frames

Total count of received frames with the active error event

Total count of received frames with incorrect checksum

Total count of received fragmented frames (not related to IP fragmentation)

Total count of received frames with IP header checksum error

Total count of received jabbed packets-a packet that is transmitted longer than the maximum packet length

Total count of received frames with frame length error

Total count of received multicast frames

Total count of received overflowed frames can be caused when device resources are insufficient to receive a certain frame

Total count of received pause frames

Total count of received frames shorter than the minimum 64 bytes, is usually caused by collisions

Total count of received frames with TCP header checksum error

Total count of received frames that were larger than the maximum supported frame size by the network device, see the max-l2mtu property

Total count of the received frame shorter than the minimum 64 bytes

Total count of received frames with UDP header checksum error

Total count of received unicast frames

Total count of received frames with unknown Ethernet protocol

Total count of transmitted 64 byte frames

Total count of transmitted 65 to 127 byte frames

Total count of transmitted 128 to 255 byte frames

Total count of transmitted 256 to 511 byte frames

Total count of transmitted 512 to 1023 byte frames

tx-1024-1518 (integer)

tx-1519-max (integer)

tx-align-error (integer)

tx-broadcast (integer)

tx-bytes (integer)

tx-collision (integer)

tx-control (integer)

tx-deferred (integer)

tx-drop (integer)

tx-excessive-collision (integer)

tx-excessive-deferred (integer)

tx-fcs-error (integer)

tx-fragment (integer)

tx-carrier-sense-error (integer)

tx-late-collision (integer)

tx-multicast (integer)

tx-multiple-collision (integer)

tx-overflow (integer)

tx-pause (integer)

tx-all-queue-drop-byte (integer)

tx-all-queue-drop-packet (integ er)

tx-queueX-byte (integer)

tx-queueX-packet (integer)

tx-runt (integer)

tx-too-short (integer)

tx-rx-64 (integer)

tx-rx-64-127 (integer)

tx-rx-128-255 (integer)

tx-rx-256-511 (integer)

tx-rx-512-1023 (integer)

tx-rx-1024-max (integer)

tx-single-collision (integer)

tx-too-long (integer)

tx-underrun (integer)

tx-unicast (integer)

Total count of transmitted 1024 to 1518 byte frames

Total count of transmitted frames larger than 1519 bytes

Total count of transmitted align error events-packets where bits are not aligned along octet boundaries

Total count of transmitted broadcast frames

Total count of transmitted bytes

Total count of transmitted frames that made collisions

Total count of transmitted control or pause frames

Total count of transmitted frames that were delayed on its first transmit attempt due to already busy medium

Total count of transmitted frames that were dropped due to the already full output queue

Total count of transmitted frames that already made multiple collisions and never got successfully transmitted

Total count of transmitted frames that were deferred for an excessive period of time due to an already busy medium

Total count of transmitted frames with incorrect checksum

Total count of transmitted fragmented frames (not related to IP fragmentation)

Total count of transmitted frames with carrier sense error

Total count of transmitted frames that made collision after being already halfway transmitted

Total count of transmitted multicast frames

Total count of transmitted frames that made more than one collision and subsequently transmitted successfully

Total count of transmitted overflowed frames

Total count of transmitted pause frames

Total count of transmitted bytes dropped by all output queues

Total count of transmitted packets dropped by all output queues

Total count of transmitted bytes on a certain queue, the X should be replaced with a queue number

Total count of transmitted frames on a certain queue, the X should be replaced with a queue number

Total count of transmitted frames shorter than the minimum 64 bytes, is usually caused by collisions

Total count of transmitted frames shorter than the minimum 64 bytes

Total count of transmitted and received 64 byte frames

Total count of transmitted and received 64 to 127 byte frames

Total count of transmitted and received 128 to 255 byte frames

Total count of transmitted and received 256 to 511 byte frames

Total count of transmitted and received 512 to 1023 byte frames

Total count of transmitted and received frames larger than 1024 bytes

Total count of transmitted frames that made only a single collision and subsequently transmitted successfully

Total count of transmitted packets that were larger than the maximum packet size

Total count of underrun frames which can be caused when device resources are insufficient to transmit a certain frame

Total count of transmitted unicast frames

For example, the output of Ethernet stats on the hAP ac2 device:

[admin@MikroTik] > /interface ethernet print stats name: ether1 ether2 ether3 ether4 ether5 driver-rx-byte: 182 334 805 898 0 5 836 927 820 24 895 692 0 driver-rx-packet: 4 449 562 546 0 4 320 155 362 259 449 0 driver-tx-byte: 15 881 099 971 0 70 502 669 211 60 498 056 53 driver-tx-packet: 52 724 428 0 54 231 229 106 498 1 rx-bytes: 178 663 398 808 0 5 983 590 739 1 358 140 795 0 rx-too-short: 0 0 0 0 0 rx-64: 12 749 144 0 362 459 125 917 0 rx-65-127: 9 612 406 0 20 366 513 292 189 0 rx-128-255: 6 259 883 0 1 672 588 261 013 0 rx-256-511: 2 950 578 0 211 380 278 147 0 rx-512-1023: 3 992 258 0 185 666 163 241 0 rx-1024-1518: 119 034 611 0 2 796 559 696 254 0 rx-1519-max: 0 0 0 0 0 rx-too-long: 0 0 0 0 0 rx-broadcast: 12 025 189 0 1 006 377 64 178 0 rx-pause: 0 0 0 0 0 rx-multicast: 4 687 869 0 36 188 220 136 0 rx-fcs-error: 0 0 0 0 0 rx-align-error: 0 0 0 0 0 rx-fragment: 0 0 0 0 0 rx-overflow: 0 0 0 0 0 tx-bytes: 16 098 535 973 0 72 066 425 886 225 001 772 0 tx-64: 1 063 375 0 924 855 37 877 0 tx-65-127: 26 924 514 0 2 442 200 959 209 0 tx-128-255: 14 588 113 0 924 746 295 961 0 tx-256-511: 1 323 733 0 1 036 515 33 252 0 tx-512-1023: 1 287 464 0 2 281 554 3 625 0 tx-1024-1518: 7 537 154 0 48 212 304 64 659 0 tx-1519-max: 0 0 0 0 0 tx-too-long: 0 0 0 0 0 tx-broadcast: 590 0 145 800 823 038 0 tx-pause: 0 0 0 0 0 tx-multicast: 0 0 1 039 243 41 716 0 tx-underrun: 0 0 0 0 0 tx-collision: 0 0 0 0 0 tx-excessive-collision: 0 0 0 0 0 tx-multiple-collision: 0 0 0 0 0 tx-single-collision: 0 0 0 0 0 tx-excessive-deferred: 0 0 0 0 0 tx-deferred: 0 0 0 0 0 tx-late-collision: 0 0 0 0 0

|1G SFP 40G QSFP+ 100G QSFP28 S-RJ01 10 Gigabit Ethernet S+RJ10 QSFP+ QSFP28 QSFP56 QSFP56-DD refer to the Ethernet user manual. manual. 1G SFP|10G SFP+/25G SFP28 400G QSFP56-DD CRS312-4C+8XG|MikroTik wired interface compatibility MikroTik SFP/SFP+/SFP28/QSFP+/QSFP28/QSFP56-DD compatibility SFP interface compatibility with 100M optical transceivers SFP+ interface compatibility with 1G optical transceivers SFP+ interface compatibility with 10G/25G optical transceivers SFP+/SFP28 interface compatibility with 2.5G transceivers QSFP+/QSFP28/QSFP56/QSFP56-DD interface supported link rates QSFP+/QSFP28 interface compatibility with breakout cables|with transceiver multi-source agreement (MSA) they should be compatible with MikroTik.|MikroTik SFP/SFP+/SFP28/QSFP+/QSFP28/QSFP56-DD compatibility compatibility tables that provide valuable insights into which transceivers are suitable for use with MikroTik devices. Additionally, some practical|This article shows the compatibility of MikroTik devices with SFP, SFP+, SFP28, QSFP+, QSFP28 and QSFP56-DD transceivers. It features detailed MikroTik devices and SFP, SFP+, SFP28, QSFP+, QSFP28 and QSFP56-DD modules do not have any restrictions for other vendor equipment. While MikroTik cannot ensure full compatibility with modules from all manufacturers, as long as the other vendor modules and devices comply RouterOS uses a disabled FEC mode as the default setting for SFP28 and QSFP28 interfaces. To ensure a successful link with other vendor devices, you may need to enable FEC mode by configuring it to either fec74 or fec91. For more information please refer to the Ethernet user||outerOS CLI to set different data transmission rates. For more detailed descriptions of properties, please configuration examples are provided using the R||||
|---|---|---|---|---|---|---|---|---|---|---|
|Model|S- RJ01|S- 85DLC05D|S- 31DLC20D|S- 3553LC20D|S- 55DLC80D|S- 4554LC80D|SFP CWDM|SFP 1m/3m DAC|S+AO0005 AOC|SFP28 1m/3m DAC|
|CCR1072-1G-8S+|+|+|+|+|+|+|+|+|+|+|
|CCR1036-12G-4S|+|+|+|+|+|+|+|+|+|+|
|CCR1036-8G-2S+|+|+|+|+|+|+|+|+|+|+|
|CCR1016-12S-1S+|+ 1|+ 1|+ 1|+ 1|+ 1|+ 1|+|+|+|+|
|CCR1009-7G-1C|+|+|+|+|+|+|+|+|+|+|
|CCR1009-8G-1S-1S+|+|+|+|+|+|+|+|+|+|+|
|CCR1009-7G-1C-1S+|+|+|+|+|+|+|+|+|+|+|
|CCR2004-1G-2XS-PCIe|-|-|-|-|-|-|-|-|-|-|
|CCR2004-1G-12S+2XS|+|+|+|+|+|+|+|+|+|+|
|CCR2004-16G-2S+|+|+|+|+|+|+|+|+|+|+|
|CCR2116-12G-4S+|+|+|+|+|+|+|+|+|+|+|
|CCR2216-1G-12XS-2XQ|+|+|+|+|+|+|+|+|+|+|

|CRS310-1G-5S-4S+/netFiber 9|||+||+||+||+||+||+|+||+||+||+||
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
|CRS310-8G+2S+IN|||+||+||+||+||+||+|+||+||+||+||
|CRS812-8DS-2DQ-2DDQ|||+||+||+||+||+||+|+||+||+||+||
|CRS804-4DDQ|10G SFP+/25G SFP28||-||-||-||-||-||-|-||-||-||-||
|Model|S+R J10|S+85DLC 03D||10D|S+31DLC|S+2332L C10D|SFP+ CWDM|DAC|SFP+ 1m/3m|S+AO0005 AOC||0003-XS+|Q+BC0003-S+ / XQ+BC|DQ+BC0003 -DS+||SFP28 1m/3m DAC|SFP28 XS+31 LC10D||SFP28 XS+2733 LC15D||SFP28 XS+85 LC01D|
|CCR1072-1G-8S+|+|+||+||+|+|+||+||+ 5||+ 5|+||+||+||+|
|CCR1036-12G-4S|-|+||+||+|+|+||+||-||-|+||+||+||+|
|CCR1036-8G-2S+|+|+||+||+|+|+||+||+ 5||+ 5|+||+||+||+|
|CCR1016-12S-1S+|+ 10|+||+||+|+|+||+||+ 1,5||+ 1,5|+||+||+||+|
|CCR1009-7G-1C|-|+||+||+|+|+||+||-||-|+||+||+||+|
|CCR1009-8G-1S-1S+|+ 10|+||+||+|+|+||+||+ 5||+ 5|+||+||+||+|
|CCR1009-7G-1C-1S+|+|+||+||+|+|+||+||+ 5||+ 5|+||+||+||+|
|CCR2004-1G-2XS- PCIe|+|+||+||+|+|+||+||+ 5||+ 5|+||+||+||+|
|CCR2004-1G- 12S+2XS|+ 11|+||+||+|+|+||+||+ 5||+ 5|+||+||+||+|
|CCR2004-16G-2S+|+|+||+||+|+|+||+||+ 5||+ 5|+||+||+||+|
|CCR2116-12G-4S+|+|+||+||+|+|+||+||+ 5||+ 5|+||+||+||+|
|CCR2216-1G-12XS- 2XQ|+|+||+||+|+|+||+||+||+|+||+||+||+|
|RDS2216-2XG- 4S+4XS-2XQ|+|+||+||+|+|+||+||+||+|+||+||+||+|
|CRS125-24G-1S|-|+||+||+|+|+||+||-||-|+||+||+||+|
|CRS305-1G-4S+|+ 7|+||+||+|+|+||+||+ 5||+ 5|+||+||+||+|
|CRS309-1G-8S+|+ 4|+||+||+|+|+||+||+ 5||+ 5|+||+||+||+|
|CRS312-4C+8XG|+|+||+||+|+|+||+||+ 5||+ 5|+||+||+||+|
|CRS318-1Fi-15Fr-2S|-|+||+||+|+|+||+||-||-|+||+||+||+|
|CRS318-16P-2S+|+|+||+||+|+|+||+||+ 5||+ 5|+||+||+||+|
|CSS318-16G-2S+|+|+||+||+|+|+||+||+ 5||+ 5|+||+||+||+|
|CRS320-8P-8B-4S+|+|+||+||+|+|+||+||+||+|+||+||+||+|
|CRS326- 4C+20G+2Q+|+|+||+||+|+|+||+||+||+|+||+||+||+|
|CRS326-24S+2Q+|+ 6|+||+||+|+|+||+||+||+|+||+||+||+|
|CRS354-48G/P- 4S+2Q+|+|+||+||+|+|+||+||+||+|+||+||+||+|
|CRS418-8P-8G-2S+|+|+||+||+|+|+||+||+||+|+||+||+||+|
|CRS520-4XS-16XQ|+|+||+||+|+|+||+||+||+|+||+||+||+|
|CRS518-16XS-2XQ|+|+||+||+|+|+||+||+||+|+||+||+||+|
|CRS510-8XS-2XQ|+|+||+||+|+|+||+||+||+|+||+||+||+|
|CSS/CRS326-24G- 2S+|+|+||+||+|+|+||+||+ 5||+ 5|+||+ 9||+ 9||+|
|CRS317-1G-16S+|+ 3|+||+||+|+|+||+||+ 5||+ 5|+||+||+||+|
|CRS328-4C-20S-4S+|+ 10|+||+||+|+|+||+||+ 5||+ 5|+||+||+||+|
|CRS328-24P-4S+|+|+||+||+|+|+||+||+ 5||+ 5|+||+ 9||+ 9||+|
|CRS226-24G-2S+|+|+||+||+|+|+||+||+ 5||+ 5|+||+||+||+|
|CRS212-1G-10S-1S+|+ 10|+||+||+|+|+||+||+ 5||+ 5|+||+||+||+|
|CRS210-8G-2S+|+|+||+||+|+|+||+||+ 5||+ 5|+||+||+||+|
|CRS112-8G/P-4S|-|+||+||+|+|+||+||-||-|+||+||+||+|
|CRS109-8G-1S|-|+||+||+|+|+||+||-||-|+||+||+||+|
|CRS106-1C-5S /FiberBox|-|+||+||+|+|+||+||-||-|+||+||+||+|
|RB5009|+|+||+||+|+|+||+||+ 5||+ 5|+||+||+||+|
|RB4011|+|+||+||+|+|+||+||+||+|+||+||+||+|
|RB3011|-|+||+||+|+|+||+||-||-|+||+||+||+|
|RB2011|-|+||+||+|+|+||+||-||-|+||+||+||+|

CRS510-8XS-2XQ + + + + + + + CRS518-16XS-2XQ + + + + + + + CRS520-4XS-16XQ + + + + + + + CCR2216-1G-12XS-2XQ + + + + + + + RDS2216-2XG-4S+4XS-2XQ + + + + + + + CRS812-8DS-2DQ-2DDQ + + + + + + + CRS804-4DDQ + + + + + + +

### 400G QSFP56-DD

|Model|DDQ+DA0001|DDQ+DA0003|DDQ+85MP01D|
|---|---|---|---|
|CRS812-8DS-2DQ-2DDQ|+|+|+|
|CRS804-4DDQ|+|+|+|
|Legend||||
|Color codes:|Check notes below|||

Not supported

Notes:

1. CCR1016-12S-1S+, CRS212-1G-10S-1S+ the SFP+1 interface does not work on any other link speed than 10G (does not support 1.25 G fiber optic transceivers)
2. CRS226-24G-2S+, CRS210-8G-2S+ - the SFP+1 interface also supports SFP 1.25G fiber optic transceivers, SFP+2 works only with 10G transceivers/links.
3. CSS/CRS317-1G-16S+ - power controller supports up to 10 simultaneous S+RJ10 modules.
4. CSS/CRS309-1G-8S+ - supports up to 4 simultaneous S+RJ10 modules. We do not recommend using S+RJ10 in passive cooling devices without additional cooling, as they have relatively high power consumption and in turn high operating temperature.
5. Q+BC0003-S+, XQ+BC0003-XS+, DQ+BC0003-DS+ - SFP+ connector support in the SFP+/SFP28 cages
6. CSS/CRS326-24S+2Q+ - supports up to 12 simultaneous S+RJ10 modules
7. CSS/CRS305-1G-4S+ - supports up to 2 simultaneous S+RJ10 modules.
8. RBFTC11 - works connected to other device 1G SFP port.
9. XS+31LC10D, XS+2733LC15D-full support has been added to CSS/CRS326-24G-2S+ and CRS328-24P-4S+ switches manufactured from October 2021.
10. S+RJ10 - support in the SFP+ cages.
11. CCR2004-1G-12S+2XS-supports up to 6 simultaneous S+RJ10 modules.
12. CCR2004-1G-2XS-PCIe-supports only the same speed in both SFP28 ports (2 x 25G or 2 x 10G modes).
13. CRS504-4XQ-OUT-reduce IP code from IP66 to IP54.
14. 10G SFP+/25G SFP28 modules-device SFP supports up to 2.5G rate, manual speed setting required to work.
15. CRS312-4C+8XG, CRS326-4C+20G+2Q+ - Combo SFP+ interfaces support 1G and 10G speeds (do not support 2.5G and 5G)
## S-RJ01

Table that states in what link rates if mounted in specific MikroTik devices S-RJ01 module will be able to work. Use these modules only with auto- negotiation enabled, forced link speeds are not supported. They will negotiate to correct duplex and highest possible rate.

|Model|
|---|
|RB5009|
|RB4011|
|RB3011|
|RB922|
|RB921|
|hAP ac|

1000 100 10 + + + + + + + + + + + + + + + + + +

|hEX PoE|+|+|+|
|---|---|---|---|
|hEX S|+|-|-|
|RB953|+/+|-/+|-/+|
|RB2011|+|-|-|
|RB260/CSS106|+|-|-|
|RBFTC11|+|-|-|
|LHG XL 52 ac|-|-|-|
|RBD22/D23 mANTBox 52 15s/NetMetal ac²|-|-|-|
|CRS106|+|+|+|
|CRS112|+|+|+|
|CRS125/CRS109|+|+|+|
|CRS212|+|+|+|
|CRS226/CRS210|-|-|-|
|CSS/CRS305-1G-4S+|+|+|+|
|CSS/CRS309-1G-8S+|+|+|+|
|CRS318-1Fi-15Fr-2S|+|+|+|
|CRS318-16P-2S+|+|+|+|
|CSS/CRS326-24G-2S+|+|+|+|
|CRS354|+|+|+|
|CSS/CRS328-4C-20S-4S+|+|+|+|
|CSS/CRS328-24P-4S+|+|+|+|
|CSS/CRS317-1G-16S+|+|+|+|
|CRS326-4C+20G+2Q+|+|+|+|
|CRS326-24S+2Q+|+|+|+|
|CSS610|+|+|+|
|FTC11XG|+|+|+|
|CRS310-1G-5S-4S+/netFiber 9|+|+|+|
|CRS310-8G+2S+IN|+|+|+|
|CCR1009|+/+|+/+|+/+|
|CCR1016-12S-1S+|+|+|+|
|CCR1036-12G-4S|+|+|+|
|CCR1036-8G-2S+|+|+|+|
|CCR1072-1G-8S+ Notes Rate works fine: + Rate does not work: - RB953: SFP1/SFP2 CCR1009: SFP+/SFP 10 Gigabit Ethernet|+|+|+|
|Speed|Cable type|S+RJ10 to Ethernet port||
|10BASE-T 100BASE-T 1000BASE-T 2.5GBASE-T 2.5GBASE-T 5GBASE-T 10GBASE-T|Cat5e/6 Cat5e/6 Cat5e/6 Cat5e/6 UTP Cat5e/6 STP Cat5e/6 Cat6/7 Actual link speed reporting;|100m 100m 100m 100m 100m 100m 30m The negotiated speed is highly dependent on the quality and length of the cables used. S+RJ10 to S+RJ10 will always negotiate to the highest possible rate. The latest revision of S+RJ10 contains "/r2" by the end of serial number. It comes with following improvements: Jumbo frames up to 10218 Bytes at 2.5G, 5G and 10G speeds; DDM monitoring (Supply Voltage, Module temperature).||
|Link Speed|Max MTU|||
|10Gbps 5Gbps 2.5Gbps 1000Mbps 100Mbps 10Mbps CRS312-4C+8XG|10218 10218 10218 1504 1504 1504 10GE ports maximum supported cable length.|||
|Speed|Cable type|10 Gigabit Ethernet ports||
|10BASE-T 100BASE-T 1000BASE-T 2.5GBASE-T 5GBASE-T 10GBASE-T|Cat5e/6 Cat5e/6 Cat5e/6 Cat5e/6 Cat5e/6 Cat6/7|100m 100m 100m 100m 100m 30m||

The negotiated speed is highly dependent on the quality and length of the cables used.

10GE ports do not support half-duplex mode with forced link speeds.

## SFP interface compatibility with 100M optical transceivers

SFP interface on the listed devices is compatible with fast ethernet fiber links.

Compatible devices (interface):

CCR1009-7G-1C (combo1) CCR1009-7G-1C-1S+ (combo1) CRS106-1C-5S (combo1) CRS328-4C-20S-4S+ (combo1 - combo4 and SFP1 - SFP20) LHG XL 52 ac RBD22/D23/mANTBox 52 15s/NetMetal ac²

## SFP+ interface compatibility with 1G optical transceivers

For MikroTik devices with SFP+ interface that support both 10G and 1G link rate, following settings must be set on both linked devices for required interfaces. These settings only relate when optical SFP transceivers are used. In order to get them working in 1G link rate, use the following configuration:

# Since RouterOS v7.12 /interface ethernet set sfp-sfpplus1 auto-negotiation=no speed=1G-baseX

# Older RouterOS /interface ethernet set sfp-sfpplus1 auto-negotiation=no speed=1Gbps full-duplex=yes

auto-negotiation disabled port speed 1G full-duplex

Devices which SFP+ ports support 1G links:

CCR2004-1G-12S+2XS-All SFP+ interfaces can be used in 1G mode if required. CCR2004-16G-2S+ - All SFP+ interfaces can be used in 1G mode if required. CCR1072-1G-8S+ - All SFP+ interfaces can be used in 1G mode if required. CCR1036-8G-2S+ - All SFP+ interfaces can be used in 1G mode if required. CCR1009-8G-1S-1S+ - All SFP+ interfaces can be used in 1G mode if required. CCR1009-7G-1C-1S+ - All SFP+ interfaces can be used in 1G mode if required. CSS3xx series switches-All SFP+ interfaces can be used in 1G mode if required. CRS3xx series switches-All SFP+ interfaces can be used in 1G mode if required. RB5009 series-SFP+1 interface can be used in 1G mode if required. RB4011 series-SFP+1 interface can be used in 1G mode if required. CRS226-24G-2S+ - Only SFP+1 supports 1G link speed, SFP+2 is for 10G links only. CRS210-8G-2S+ - Only SFP+1 supports 1G link speed, SFP+2 is for 10G links only. CSS610 series switches-All SFP+ interfaces can be used in 1G mode if required. FTC11XG-SFP+1 interface can be used in 1G mode if required.

Devices which SFP+ interfaces can be used only for 10G links:

CCR1016-12S-1S+ CRS212-1G-10S-1S+

## SFP+ interface compatibility with 10G/25G optical transceivers

MikroTik devices with SFP+ ports can establish 10G links using 10G/25G optical fiber transceivers, however additional SFP Rate Select setting must be configured to avoid data corruption during transmission. The following settings are required on the SFP+ interface:

# Since RouterOS v7.12 /interface ethernet set sfp-sfpplus1 auto-negotiation=no speed=10G-baseSR-LR sfp-rate-select=low

# Older RouterOS /interface ethernet set sfp-sfpplus1 auto-negotiation=no speed=10Gbps full-duplex=yes sfp-rate-select=low

This requirement applies to MikroTik 10G/25G modules:

XS+31LC10D XS+2733LC15D

## SFP+/SFP28 interface compatibility with 2.5G transceivers

The 2.5G link rate support is implemented since RouterOS v7.3. MikroTik devices with SFP+ and SFP28 interfaces that support 2.5G link rate require following settings to be set on both linked device interfaces.

# Since RouterOS v7.12 /interface ethernet set sfp-sfpplus1 auto-negotiation=no speed=2.5G-baseX

# Older RouterOS /interface ethernet set sfp-sfpplus1 auto-negotiation=no speed=2.5Gbps full-duplex=yes

auto-negotiation disabled port speed 2.5G full-duplex

Devices which support 2.5G links in SFP/SFP+/SFP28 ports:

CRS3xx series switches-All SFP+ interfaces can be used in 2.5G mode if required. CCR2004-1G-12S+2XS-All SFP+ and SFP28 interfaces can be used in 2.5G mode if required. CCR2116-12G-4S+ - All SFP+ interfaces can be used in 2.5G mode if required. CRS5xx series-All SFP28 interfaces can be used in 2.5G mode if required. CCR2216-1G-12XS-2XQ-All SFP28 interfaces can be used in 2.5G mode if required. RB5009 series-SFP+ interface can be used in 2.5G mode if required. L009 series-SFP interface can be used in 2.5G mode if required. L23 series-SFP interface can be used in 2.5G mode if required. CSS610 series switches-All SFP+ interfaces can be used in 2.5G mode if required. FTC11XG-SFP+1 interface can be used in 2.5G mode if required. E60/E62 - SFP interface can be used in 2.5G mode if required.

## QSFP+/QSFP28/QSFP56/QSFP56-DD interface supported link rates

In RouterOS, QSFP+, QSFP28, QSFP56 and QSFP56-DD interfaces are designed to handle high-speed data transmission by utilizing multiple channels. Each QSFP+, QSFP28 or QSFP56 interface is divided into four sub-interfaces and QSFP56-DD is divided into eight sub-interfaces, each corresponding to a transmission channel necessary for proper operation.

The naming convention for QSFP+, QSFP28, QSFP56 and QSFP56-DD sub-interfaces includes two parts:

The first digit following "qsfpplus", "qsfp28-", "qsfp56-" or "qsfp56-dd-" represents the QSFP+, QSFP28, QSFP56 or QSFP56-DD physical port. The second digit, ranging from 1 to 4 for QSFP+, QSFP28, QSFP56 and from 1 to 8 for QSFP56-DD, denotes each of the individual channels.

Below are examples of how QSFP+, QSFP28, QSFP56 and QSFP56-DD interfaces appear in RouterOS:

# QSFP+ /interface ethernet print Flags: R-RUNNING Columns: NAME, MTU, MAC-ADDRESS, ARP, SWITCH # NAME MTU MAC-ADDRESS ARP SWITCH 1 qsfpplus1-1 1500 48:8F:5A:B6:09:8C enabled switch1 2 qsfpplus1-2 1500 48:8F:5A:B6:09:8D enabled switch1 3 qsfpplus1-3 1500 48:8F:5A:B6:09:8E enabled switch1 4 qsfpplus1-4 1500 48:8F:5A:B6:09:8F enabled switch1

# QSFP28 /interface ethernet print Flags: R-RUNNING Columns: NAME, MTU, MAC-ADDRESS, ARP, SWITCH # NAME MTU MAC-ADDRESS ARP SWITCH 1 qsfp28-1-1 1500 DC:2C:6E:9E:11:14 enabled switch1 2 qsfp28-1-2 1500 DC:2C:6E:9E:11:15 enabled switch1 3 qsfp28-1-3 1500 DC:2C:6E:9E:11:16 enabled switch1 4 qsfp28-1-4 1500 DC:2C:6E:9E:11:17 enabled switch1

# QSFP56 /interface/ethernet/print Flags: R-RUNNING; S-SLAVE Columns: NAME, MTU, MAC-ADDRESS, ARP, SWITCH # NAME MTU MAC-ADDRESS ARP SWITCH 2 qsfp56-1-1 1500 04:F4:1C:1A:82:A1 enabled switch1 3 qsfp56-1-2 1500 04:F4:1C:1A:82:A2 enabled switch1 4 qsfp56-1-3 1500 04:F4:1C:1A:82:A3 enabled switch1 5 qsfp56-1-4 1500 04:F4:1C:1A:82:A4 enabled switch1

# QSFP56-DD /interface/ethernet/print Flags: R-RUNNING; S-SLAVE Columns: NAME, MTU, MAC-ADDRESS, ARP, SWITCH # NAME MTU MAC-ADDRESS ARP SWITCH 10 qsfp56-dd-1-1 1500 04:F4:1C:1A:82:91 enabled switch1 11 qsfp56-dd-1-2 1500 04:F4:1C:1A:82:92 enabled switch1 12 qsfp56-dd-1-3 1500 04:F4:1C:1A:82:93 enabled switch1 13 qsfp56-dd-1-4 1500 04:F4:1C:1A:82:94 enabled switch1 14 qsfp56-dd-1-5 1500 04:F4:1C:1A:82:95 enabled switch1 15 qsfp56-dd-1-6 1500 04:F4:1C:1A:82:96 enabled switch1 16 qsfp56-dd-1-7 1500 04:F4:1C:1A:82:97 enabled switch1 17 qsfp56-dd-1-8 1500 04:F4:1C:1A:82:98 enabled switch1

Configuration and monitoring for these sub-interfaces may vary based on factors such as auto-negotiation, advertised speeds, and the type of transceiver (e.g., break-out cable or single fiber). The following sections will provide guidance on the configuration necessary for each use case.

Disabling or enabling any of the physical port sub-interfaces will trigger a reconfiguration of the entire port group, restarting all channels.

QSFP+

For MikroTik CRS3xx series devices, QSFP+ interfaces support the following link speeds:

1x 40G 4x 10G 4x 1G

Link Configuration:

40G: Can be configured with either auto-negotiation or a forced 40G speed. 4x10G and 4x1G: Must be set with a forced speed mode and auto-negotiation disabled.

Starting from RouterOS version 7.12, in addition to choosing the right transmission rate, it's important to specify the correct link mode. For example, you might use CR4 for DAC(Direct Attach Copper) or SR4-LR4 for optical fiber.

Configuration Examples:

For RouterOS v7.12 and later:

# 1x40G-DAC /interface ethernet set qsfpplus1-1 auto-negotiation=no speed=40G-baseCR4

# 1x40G-Optical /interface ethernet set qsfpplus1-1 auto-negotiation=no speed=40G-baseSR4-LR4

# 4x10G-DAC /interface ethernet set qsfpplus1-1 auto-negotiation=no speed=10G-baseCR /interface ethernet set qsfpplus1-2 auto-negotiation=no speed=10G-baseCR /interface ethernet set qsfpplus1-3 auto-negotiation=no speed=10G-baseCR /interface ethernet set qsfpplus1-4 auto-negotiation=no speed=10G-baseCR

# 4x10G-Optical /interface ethernet set qsfpplus1-1 auto-negotiation=no speed=10G-baseSR-LR /interface ethernet set qsfpplus1-2 auto-negotiation=no speed=10G-baseSR-LR /interface ethernet set qsfpplus1-3 auto-negotiation=no speed=10G-baseSR-LR /interface ethernet set qsfpplus1-4 auto-negotiation=no speed=10G-baseSR-LR

In single-link mode, only the first QSFP+ sub-interface needs to be configured, while the remaining sub-interfaces should remain enabled.

For RouterOS versions earlier than v7.12:

# 1x40G-DAC/Optical /interface ethernet set qsfpplus1-1 auto-negotiation=no speed=40Gbps full-duplex=yes

# 4x10G-DAC/Optical /interface ethernet set qsfpplus1-1 auto-negotiation=no speed=10Gbps full-duplex=yes /interface ethernet set qsfpplus1-2 auto-negotiation=no speed=10Gbps full-duplex=yes /interface ethernet set qsfpplus1-3 auto-negotiation=no speed=10Gbps full-duplex=yes /interface ethernet set qsfpplus1-4 auto-negotiation=no speed=10Gbps full-duplex=yes

QSFP28

For MikroTik CRS5xx series and CCR2216 devices, QSFP28 interfaces support the following link speeds:

1x 100G 2x 50G (available since RouterOS v7.12) 1x 40G 4x 25G 4x 10G 4x 1G

Not supported: 50G over single channel, 2x 40G

Link Configuration:

100G: Can be configured with either auto-negotiation or a forced 100G speed. 2x50G, 1x40G, 4x25G, 4x10G, and 4x1G: Must be set with a forced speed mode and auto-negotiation disabled.

Starting from RouterOS version 7.12, in addition to choosing the right transmission rate, it's important to specify the correct link mode. For example, you might use CR4 for DAC(Direct Attach Copper) or SR4-LR4 for optical fiber.

Configuration Examples:

For RouterOS v7.12 and later:

# 1x100G-DAC /interface ethernet set qsfp28-1-1 auto-negotiation=no speed=100G-baseCR4

# 1x100G-Optical /interface ethernet set qsfp28-2-1 auto-negotiation=no speed=100G-baseSR4-LR4

# 2x50G-DAC /interface ethernet set qsfp28-1-1 auto-negotiation=no speed=50G-baseCR2 /interface ethernet set qsfp28-1-3 auto-negotiation=no speed=50G-baseCR2

# 2x50G-Optical /interface ethernet set qsfp28-1-1 auto-negotiation=no speed=50G-baseSR2-LR2 /interface ethernet set qsfp28-1-3 auto-negotiation=no speed=50G-baseSR2-LR2

# 4x25G-DAC /interface ethernet set qsfp28-1-1 auto-negotiation=no speed=25G-baseCR /interface ethernet set qsfp28-1-2 auto-negotiation=no speed=25G-baseCR /interface ethernet set qsfp28-1-3 auto-negotiation=no speed=25G-baseCR /interface ethernet set qsfp28-1-4 auto-negotiation=no speed=25G-baseCR

# 4x25G-Optical /interface ethernet set qsfp28-1-1 auto-negotiation=no speed=25G-baseSR-LR /interface ethernet set qsfp28-1-2 auto-negotiation=no speed=25G-baseSR-LR /interface ethernet set qsfp28-1-3 auto-negotiation=no speed=25G-baseSR-LR /interface ethernet set qsfp28-1-4 auto-negotiation=no speed=25G-baseSR-LR

In single-link mode, only the first QSFP28 sub-interface needs to be configured, while the remaining sub-interfaces should remain enabled. Similarly, for 2x50G link mode, only the master interfaces (e.g., qsfp28-1-1 and qsfp28-1-3) need to be configured, but the other sub-interfaces must remain enabled.

For RouterOS versions earlier than v7.12:

# 1x100G-DAC/Optical /interface ethernet set qsfp28-1-1 auto-negotiation=no speed=100Gbps full-duplex=yes

# 4x25G-DAC/Optical /interface ethernet set qsfp28-1-1 auto-negotiation=no speed=25Gbps full-duplex=yes /interface ethernet set qsfp28-1-2 auto-negotiation=no speed=25Gbps full-duplex=yes /interface ethernet set qsfp28-1-3 auto-negotiation=no speed=25Gbps full-duplex=yes /interface ethernet set qsfp28-1-4 auto-negotiation=no speed=25Gbps full-duplex=yes

QSFP56

For MikroTik CRS812 device, QSFP56 interfaces support the following link speeds:

1x 200G 2x 100G 4x 50G 1x 100G 2x 50G 1x 40G 4x 25G 4x 10G 4x 1G

Link Configuration:

200G: Can be configured with either auto-negotiation or a forced 200G speed. 2x100G, 4x50G, 1x100G,  2x50G, 1x40G, 4x25G, 4x10G and 4x1G: Must be set with a forced speed mode and auto-negotiation disabled.

It's important to specify the correct link mode. For example, you might use CR4 for DAC(Direct Attach Copper) or SR4-LR4 for optical fiber.

Configuration Examples:

# 1x200G-DAC /interface ethernet set qsfp56-1-1 auto-negotiation=no speed=200G-baseCR4

# 1x200G-Optical /interface ethernet set qsfp56-1-1 auto-negotiation=no speed=200G-baseSR4-LR4

# 2x100G-DAC /interface ethernet set qsfp56-1-1 auto-negotiation=no speed=100G-baseCR2 /interface ethernet set qsfp56-1-3 auto-negotiation=no speed=100G-baseCR2

# 2x100G-Optical /interface ethernet set qsfp56-1-1 auto-negotiation=no speed=100G-baseSR2-LR2 /interface ethernet set qsfp56-1-3 auto-negotiation=no speed=100G-baseSR2-LR2

# 4x50G-DAC /interface ethernet set qsfp56-1-1 auto-negotiation=no speed=50G-baseCR /interface ethernet set qsfp56-1-2 auto-negotiation=no speed=50G-baseCR /interface ethernet set qsfp56-1-3 auto-negotiation=no speed=50G-baseCR /interface ethernet set qsfp56-1-4 auto-negotiation=no speed=50G-baseCR

# 4x50G-Optical /interface ethernet set qsfp56-1-1 auto-negotiation=no speed=50G-baseSR-LR /interface ethernet set qsfp56-1-2 auto-negotiation=no speed=50G-baseSR-LR /interface ethernet set qsfp56-1-3 auto-negotiation=no speed=50G-baseSR-LR /interface ethernet set qsfp56-1-4 auto-negotiation=no speed=50G-baseSR-LR

# 1x100G-DAC /interface ethernet set qsfp56-1-1 auto-negotiation=no speed=100G-baseCR4

# 1x100G-Optical /interface ethernet set qsfp56-1-1 auto-negotiation=no speed=100G-baseSR4-LR4

# 2x50G-DAC /interface ethernet set qsfp56-1-1 auto-negotiation=no speed=50G-baseCR2 /interface ethernet set qsfp56-1-3 auto-negotiation=no speed=50G-baseCR2

# 2x50G-Optical /interface ethernet set qsfp56-1-1 auto-negotiation=no speed=50G-baseSR2-LR2 /interface ethernet set qsfp56-1-3 auto-negotiation=no speed=50G-baseSR2-LR2

# 4x25G-DAC /interface ethernet set qsfp56-1-1 auto-negotiation=no speed=25G-baseCR /interface ethernet set qsfp56-1-2 auto-negotiation=no speed=25G-baseCR /interface ethernet set qsfp56-1-3 auto-negotiation=no speed=25G-baseCR /interface ethernet set qsfp56-1-4 auto-negotiation=no speed=25G-baseCR

# 4x25G-Optical /interface ethernet set qsfp56-1-1 auto-negotiation=no speed=25G-baseSR-LR /interface ethernet set qsfp56-1-2 auto-negotiation=no speed=25G-baseSR-LR /interface ethernet set qsfp56-1-3 auto-negotiation=no speed=25G-baseSR-LR /interface ethernet set qsfp56-1-4 auto-negotiation=no speed=25G-baseSR-LR

QSFP56-DD

For MikroTik CRS812 and CRS804 devices, QSFP56-DD interfaces support the following link speeds:

1x 400G 2x 200G 4x 100G 8x 50G 8x 25G 2x 40G 8x 10G 8x 1G

Link Configuration:

400G: Can be configured with either auto-negotiation or a forced 200G speed. 2x200G, 4x100G, 8x50G,  8x25G, 2x40G, 8x10G and 8x1G: Must be set with a forced speed mode and auto-negotiation disabled.

It's important to specify the correct link mode. For example, you might use CR8 for DAC(Direct Attach Copper) or SR8-LR8 for optical fiber.

Configuration Examples:

# 1x400G-DAC /interface ethernet set qsfp56-dd-1-1 auto-negotiation=no speed=400G-baseCR8

# 1x400G-Optical /interface ethernet set qsfp56-dd-1-1 auto-negotiation=no speed=400G-baseSR8-LR8

# 2x200G-DAC /interface ethernet set qsfp56-dd-1-1 auto-negotiation=no speed=200G-baseCR4 /interface ethernet set qsfp56-dd-1-5 auto-negotiation=no speed=200G-baseCR4

# 2x200G-Optical /interface ethernet set qsfp56-dd-1-1 auto-negotiation=no speed=200G-baseSR4-LR4 /interface ethernet set qsfp56-dd-1-5 auto-negotiation=no speed=200G-baseSR4-LR4

# 4x100G-DAC /interface ethernet set qsfp56-dd-1-1 auto-negotiation=no speed=100G-baseCR2 /interface ethernet set qsfp56-dd-1-3 auto-negotiation=no speed=100G-baseCR2 /interface ethernet set qsfp56-dd-1-5 auto-negotiation=no speed=100G-baseCR2 /interface ethernet set qsfp56-dd-1-7 auto-negotiation=no speed=100G-baseCR2

# 4x100G-Optical /interface ethernet set qsfp56-dd-1-1 auto-negotiation=no speed=100G-baseSR2-LR2 /interface ethernet set qsfp56-dd-1-3 auto-negotiation=no speed=100G-baseSR2-LR2 /interface ethernet set qsfp56-dd-1-5 auto-negotiation=no speed=100G-baseSR2-LR2 /interface ethernet set qsfp56-dd-1-7 auto-negotiation=no speed=100G-baseSR2-LR2

# 8x50G-DAC /interface ethernet set qsfp56-dd-1-1 auto-negotiation=no speed=50G-baseCR /interface ethernet set qsfp56-dd-1-2 auto-negotiation=no speed=50G-baseCR /interface ethernet set qsfp56-dd-1-3 auto-negotiation=no speed=50G-baseCR /interface ethernet set qsfp56-dd-1-4 auto-negotiation=no speed=50G-baseCR /interface ethernet set qsfp56-dd-1-5 auto-negotiation=no speed=50G-baseCR /interface ethernet set qsfp56-dd-1-6 auto-negotiation=no speed=50G-baseCR /interface ethernet set qsfp56-dd-1-7 auto-negotiation=no speed=50G-baseCR /interface ethernet set qsfp56-dd-1-8 auto-negotiation=no speed=50G-baseCR

# 8x50G-Optical /interface ethernet set qsfp56-dd-1-1 auto-negotiation=no speed=50G-baseSR-LR /interface ethernet set qsfp56-dd-1-2 auto-negotiation=no speed=50G-baseSR-LR /interface ethernet set qsfp56-dd-1-3 auto-negotiation=no speed=50G-baseSR-LR /interface ethernet set qsfp56-dd-1-4 auto-negotiation=no speed=50G-baseSR-LR /interface ethernet set qsfp56-dd-1-5 auto-negotiation=no speed=50G-baseSR-LR /interface ethernet set qsfp56-dd-1-6 auto-negotiation=no speed=50G-baseSR-LR /interface ethernet set qsfp56-dd-1-7 auto-negotiation=no speed=50G-baseSR-LR /interface ethernet set qsfp56-dd-1-8 auto-negotiation=no speed=50G-baseSR-LR

# 8x25G-DAC /interface ethernet set qsfp56-dd-1-1 auto-negotiation=no speed=25G-baseCR /interface ethernet set qsfp56-dd-1-2 auto-negotiation=no speed=25G-baseCR /interface ethernet set qsfp56-dd-1-3 auto-negotiation=no speed=25G-baseCR /interface ethernet set qsfp56-dd-1-4 auto-negotiation=no speed=25G-baseCR /interface ethernet set qsfp56-dd-1-5 auto-negotiation=no speed=25G-baseCR /interface ethernet set qsfp56-dd-1-6 auto-negotiation=no speed=25G-baseCR /interface ethernet set qsfp56-dd-1-7 auto-negotiation=no speed=25G-baseCR /interface ethernet set qsfp56-dd-1-8 auto-negotiation=no speed=25G-baseCR

# 8x25G-Optical /interface ethernet set qsfp56-dd-1-1 auto-negotiation=no speed=25G-baseSR-LR /interface ethernet set qsfp56-dd-1-2 auto-negotiation=no speed=25G-baseSR-LR /interface ethernet set qsfp56-dd-1-3 auto-negotiation=no speed=25G-baseSR-LR /interface ethernet set qsfp56-dd-1-4 auto-negotiation=no speed=25G-baseSR-LR /interface ethernet set qsfp56-dd-1-5 auto-negotiation=no speed=25G-baseSR-LR /interface ethernet set qsfp56-dd-1-6 auto-negotiation=no speed=25G-baseSR-LR /interface ethernet set qsfp56-dd-1-7 auto-negotiation=no speed=25G-baseSR-LR

/interface ethernet set qsfp56-dd-1-8 auto-negotiation=no speed=25G-baseSR-LR

# 2x40G-DAC /interface ethernet set qsfp56-dd-1-1 auto-negotiation=no speed=40G-baseCR4 /interface ethernet set qsfp56-dd-1-5 auto-negotiation=no speed=40G-baseCR4

# 2x40G - Optical /interface ethernet set qsfp56-dd-1-1 auto-negotiation=no speed=40G-baseSR4-LR4 /interface ethernet set qsfp56-dd-1-5 auto-negotiation=no speed=40G-baseSR4-LR4

# 8x10G-DAC /interface ethernet set qsfp56-dd-1-1 auto-negotiation=no speed=10G-baseCR /interface ethernet set qsfp56-dd-1-2 auto-negotiation=no speed=10G-baseCR /interface ethernet set qsfp56-dd-1-3 auto-negotiation=no speed=10G-baseCR /interface ethernet set qsfp56-dd-1-4 auto-negotiation=no speed=10G-baseCR /interface ethernet set qsfp56-dd-1-5 auto-negotiation=no speed=10G-baseCR /interface ethernet set qsfp56-dd-1-6 auto-negotiation=no speed=10G-baseCR /interface ethernet set qsfp56-dd-1-7 auto-negotiation=no speed=10G-baseCR /interface ethernet set qsfp56-dd-1-8 auto-negotiation=no speed=10G-baseCR

# 8x10G-Optical /interface ethernet set qsfp56-dd-1-1 auto-negotiation=no speed=10G-baseSR-LR /interface ethernet set qsfp56-dd-1-2 auto-negotiation=no speed=10G-baseSR-LR /interface ethernet set qsfp56-dd-1-3 auto-negotiation=no speed=10G-baseSR-LR /interface ethernet set qsfp56-dd-1-4 auto-negotiation=no speed=10G-baseSR-LR /interface ethernet set qsfp56-dd-1-5 auto-negotiation=no speed=10G-baseSR-LR /interface ethernet set qsfp56-dd-1-6 auto-negotiation=no speed=10G-baseSR-LR /interface ethernet set qsfp56-dd-1-7 auto-negotiation=no speed=10G-baseSR-LR /interface ethernet set qsfp56-dd-1-8 auto-negotiation=no speed=10G-baseSR-LR

## QSFP+/QSFP28 interface compatibility with breakout cables

MikroTik devices can establish links between QSFP+/QSFP28 and SFP+/SFP28 ports using breakout cables.

Configuration Examples:

For RouterOS v7.12 and later:

# QSFP+ - DAC /interface ethernet set qsfpplus1-1 auto-negotiation=no speed=10G-baseCR /interface ethernet set qsfpplus1-2 auto-negotiation=no speed=10G-baseCR /interface ethernet set qsfpplus1-3 auto-negotiation=no speed=10G-baseCR /interface ethernet set qsfpplus1-4 auto-negotiation=no speed=10G-baseCR

# QSFP+ - Optical /interface ethernet set qsfpplus1-1 auto-negotiation=no speed=10G-baseSR-LR /interface ethernet set qsfpplus1-2 auto-negotiation=no speed=10G-baseSR-LR /interface ethernet set qsfpplus1-3 auto-negotiation=no speed=10G-baseSR-LR /interface ethernet set qsfpplus1-4 auto-negotiation=no speed=10G-baseSR-LR

# QSFP28 - DAC /interface ethernet set qsfp28-1-1 auto-negotiation=no speed=25G-baseCR /interface ethernet set qsfp28-1-2 auto-negotiation=no speed=25G-baseCR /interface ethernet set qsfp28-1-3 auto-negotiation=no speed=25G-baseCR /interface ethernet set qsfp28-1-4 auto-negotiation=no speed=25G-baseCR

# QSFP28 - Optical /interface ethernet set qsfp28-1-1 auto-negotiation=no speed=25G-baseSR-LR /interface ethernet set qsfp28-1-2 auto-negotiation=no speed=25G-baseSR-LR /interface ethernet set qsfp28-1-3 auto-negotiation=no speed=25G-baseSR-LR /interface ethernet set qsfp28-1-4 auto-negotiation=no speed=25G-baseSR-LR

It is also possible to use QSFP28 to 2x50G QSFP28 Breakout Cables:

# 2x50G-DAC /interface ethernet set qsfp28-1-1 auto-negotiation=no speed=50G-baseCR2 /interface ethernet set qsfp28-1-3 auto-negotiation=no speed=50G-baseCR2

# 2x50G-Optical /interface ethernet set qsfp28-1-1 auto-negotiation=no speed=50G-baseSR2-LR2 /interface ethernet set qsfp28-1-3 auto-negotiation=no speed=50G-baseSR2-LR2

Or to configure different speed rates for each QSFP+/QSFP28 sub-interfaces:

# QSFP28 - DAC /interface ethernet set qsfp28-1-1 auto-negotiation=no speed=25G-baseCR /interface ethernet set qsfp28-1-2 auto-negotiation=no speed=25G-baseCR /interface ethernet set qsfp28-1-3 auto-negotiation=no speed=10G-baseCR /interface ethernet set qsfp28-1-4 auto-negotiation=no speed=10G-baseCR

# QSFP28 - Optical /interface ethernet set qsfp28-1-1 auto-negotiation=no speed=25G-baseSR-LR /interface ethernet set qsfp28-1-2 auto-negotiation=no speed=25G-baseSR-LR /interface ethernet set qsfp28-1-3 auto-negotiation=no speed=10G-baseSR-LR /interface ethernet set qsfp28-1-4 auto-negotiation=no speed=10G-baseSR-LR

For RouterOS versions earlier than v7.12:

# QSFP+ - DAC/Optical /interface ethernet set qsfpplus1-1 auto-negotiation=no speed=10Gbps full-duplex=yes /interface ethernet set qsfpplus1-2 auto-negotiation=no speed=10Gbps full-duplex=yes /interface ethernet set qsfpplus1-3 auto-negotiation=no speed=10Gbps full-duplex=yes /interface ethernet set qsfpplus1-4 auto-negotiation=no speed=10Gbps full-duplex=yes

# QSFP28 - DAC/Optical /interface ethernet set qsfp28-1-1 auto-negotiation=no speed=25Gbps full-duplex=yes /interface ethernet set qsfp28-1-2 auto-negotiation=no speed=25Gbps full-duplex=yes /interface ethernet set qsfp28-1-3 auto-negotiation=no speed=25Gbps full-duplex=yes /interface ethernet set qsfp28-1-4 auto-negotiation=no speed=25Gbps full-duplex=yes
