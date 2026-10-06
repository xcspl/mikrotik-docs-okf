---
type: Reference
title: "Ethernet"
description: "For additional information about MikroTik SFP and QSFP type of interfaces and their compatibility, please refer to wired interface compatibility page."
timestamp: '2026-10-06'
status: active
tags: [routeros, mikrotik, networking]
resource: ~/Downloads/ROS-260526-1445-796.pdf
sources:
  - resource: https://manual.mikrotik.com/docs/introduction/
---

# Ethernet

Summary Auto-negotiation and Forced Link Mode Advertise Ethernet LED behavior Forced Mode FEC Properties Menu specific commands Monitor Detect Cable Problems Stats

## Summary

MikroTik RouterOS supports various types of Ethernet interfaces-ranging from 10Mbps to 10Gbps Ethernet over copper twisted pair, 1Gbps, 10Gbps, 25Gbps SFP/SFP+/SFP28 interfaces and 40Gbps, 100Gbps QSFP+/QSFP28 interfaces. Certain RouterBoard devices are equipped with a combo interface that simultaneously contains two interface types (e.g. Ethernet over twisted pair and SFP/SFP+ interface) allowing to select the most suitable option or creating a physical link failover. Through RouterOS, it is possible to control different Ethernet related properties like link speed, auto-negotiation, duplex mode, etc, monitor a transceiver diagnostic information and see a wide range of Ethernet related statistics.

For additional information about MikroTik SFP and QSFP type of interfaces and their compatibility, please refer to wired interface compatibility page.

## Auto-negotiation and Forced Link Mode

Auto-negotiation is a communication method and a set of steps employed by Ethernet devices connected via twisted pair cables. It enables these devices to agree on key transmission settings, including speed, duplex mode, and flow control. During this process, the connected devices initially exchange information about their capabilities concerning these settings. Afterward, they mutually select the best possible transmission mode that both devices can support effectively.

However, in RouterOS auto-negotiation behaves differently on SFP/QSFP ports compared to standard RJ45 Ethernet ports. In the case of SFP/QSFP interfaces, the negotiation process <u>does not involve the exchange of advertised capabilities</u> (no advertisement bits are shared). Instead, RouterOS attempts to bring up the link using the highest supported mode on each side. For a successful connection, both devices must advertise the same highest common mode.

For example:

Device A advertises 10G-baseCR and 25G-baseCR. Device B advertises only 10G-baseCR.

In this case, the link will not establish, because Device A prioritizes 25G while Device B advertise only 10G.

To ensure a successful link:

Both Device A and Device B must have the same highest advertised mode. So if Device B advertises 25G-baseCR, and Device A also includes 25G-baseCR as its highest advertisement, the link will be established.

In summary, when configuring SFP/QSFP interfaces, make sure that the highest supported mode matches on both ends to ensure proper link establishment.

Advertise

Prior to RouterOS version 7.12, when auto-negotiation was enabled interfaces attempted to guess the maximum available speed of the interface on the other end (making the advertise setting inapplicable for SFP/QSFP interfaces).

After the RouterOS version 7.12, you can now manually set the advertise bits to specify the desired link modes you want to use. The speed arguments have also been revised to provide clearer representation, as the previous values were too ambiguous. Additionally, the full-duplex setting has been removed because the new link modes already encompass the duplex options(see table below).

Link Modes (for advertise and speed properties) Description

10M-baseT-half

10M-baseT-full

100M-baseT-half

100M-baseT-full

100M-baseFX-full

1G-baseT-half

1G-baseT-full

1G-baseX

2.5G-baseT
2.5G-baseX 5G-baseT 10G-baseT 10G-baseSR-LR 10G-baseCR 40G-baseSR4-LR4 40G-baseCR4 25G-baseSR-LR 25G-baseCR 50G-baseSR2-LR2 50G-baseCR2 100G-baseSR4-LR4 100G-baseCR4 50G-baseSR-LR 50G-baseCR 100G-baseSR2-LR2 100G-baseCR2 200G-baseSR4-LR4 200G-baseCR4 400G-baseSR8-LR8 400G-baseCR8
10M twisted-pair half-duplex

10M twisted-pair full-duplex

100M twisted-pair half-duplex

100M twisted-pair full-duplex

100M optical-fiber

1G twisted-pair half-duplex

1G twisted-pair full-duplex

1G optical-fiber

2.5G twisted-pair full-duplex
2.5G optical-fiber 5G twisted-pair full-duplex 10G twisted-pair full-duplex 10G optical-fiber 10G twinaxial-copper 4x10G optical-fiber 4x10G twinaxial-copper 25G optical-fiber 25G twinaxial-copper 2x25G optical-fiber 2x25G twinaxial-copper 4x25G optical-fiber 4x25G twinaxial-copper 50G optical-fiber 50G twinaxial-copper 2x50G optical-fiber 2x50G twinaxial-copper 4x50G optical-fiber 4x50G twinaxial-copper 8x50G optical-fiber 8x50G twinaxial-copper

Link Mode Naming Scheme

Transmission Rates: The first number followed by 'M' or 'G' (e.g., 10M, 100M, 1G) represents the data transmission rates in megabits or gigabits per second.

Interface Types: The symbols after "base" indicate the interface types:

T: Stands for twisted pair cabling, followed by the duplex mode (either half or full). SR-LR: Stands for "short-range" and "long-range" optical modules, including other variants like LRM, ER, ZR, etc. These link modes should be used with optical modules. CR: Stands for twin-axial copper and is used with direct attach cable (DAC). For 1Gbps DAC, the appropriate link mode is 1G-baseX. FX: Stands for Fast Ethernet over Fiber optic cable. This also includes LX-long-wavelength standard.

Number of Lines:

SR2-LR2/CR2: means two lines. SR4-LR4/CR4: means four lines. SR8-LR8/CR8: means eight lines.

Before manually configuring the advertise bits for your interface, first determine which bits are supported by executing the command /interface ethernet monitor and checking the "supported" list. You can also view the advertise bits supported by your transceiver under "sfp-supported" field. Additionally, the "advertising" will show the bits that RouterOS has automatically set. The list is generated by comparing the maximum available link mode values on your interface and transceiver and selecting the ones that match.

[admin@MikroTik] > /interface/ethernet/monitor qsfp28-1-1 name: qsfp28-1-1 supported: 10M-baseT-half,10M-baseT-full,100M-baseT-half,100M-baseT-full,1G-baseT-half,1G- baseT-full, 1G-baseX,2.5G-baseT,2.5G-baseX,5G-baseT,10G-baseT,10G-baseSR-LR,10G-baseCR,40G- baseSR4-LR4, 40G-baseCR4,25G-baseSR-LR,25G-baseCR,50G-baseSR2-LR2,50G-baseCR2,100G-baseSR4-LR4, 100G-baseCR4 sfp-supported: 10G-baseSR-LR,25G-baseSR-LR,100G-baseSR4-LR4 advertising: 10G-baseSR-LR,25G-baseSR-LR,100G-baseSR4-LR4 ...

One application where manually set advertise settings could be used is for all of sub-interfaces under QSFP. The overall configuration process starts with the topmost enabled port. If the chosen mode is valid and supported, it will be applied. If that particular link mode requires multiple lanes, the advertise and speed configuration of the next interface is ignored, but the interface should remain enabled. The next available free lane or port follows a similar process.

/interface ethernet set [ find default-name=qsfp28-1-1] advertise=50G-baseCR2 set [ find default-name=qsfp28-1-3] advertise=25G-baseCR set [ find default-name=qsfp28-1-4] advertise=25G-baseCR

Note: Multiple channels interface link modes (50G-baseCR2, 50G-baseSR2-LR2 ) can not be configured for single channel interface (SFP28

/SFP56).

Note: IEEE 802.3az Energy Efficient Ethernet (EEE) capabilities are disabled on all our products. There is no option to manually enable or

disable EEE settings.

### Ethernet LED behavior

Green LED (Link/Speed)

- On (solid) – max rate Yellow/Amber LED (Activity/Speed)

- On (solid) - link established.
- Off – No activity.
- Blinking – Data is being transmitted.
### Forced Mode

In the situation when a warning message appears in the log records after connecting the DAC cable or optical module, as example:

10:20:47 interface,warning sfp-sfpplus1 module auto-initialization failed, try forced-mode

This may indicate that the connected cable or module has a corrupted or bad EEPROM checksum, which causes the automatic connection configuration to fail. This functionality was introduced in RouterOS version 7.12 and may affect some links that worked in the past by mistake with wrongly assumed module /cable attributes, which could lead to various problems related to link connection and device functionality.

In such cases, you can attempt to set the link mode manually, and this might help establish a working link. The following forced port setting examples are provided:

For DAC cables and connection speeds of 1G/10G/25G:

/interface ethernet set [ find default-name=sfp-sfpplus1] auto-negotiation=no speed=1G-baseT-full set [ find default-name=sfp-sfpplus1] auto-negotiation=no speed=10G-baseCR set [ find default-name=sfp-sfpplus1] auto-negotiation=no speed=25G-baseCR

Note: When selecting the interface speed setting, pay attention to what rates your DAC cable supports (check cable specification data)

For optical modules and connection speeds of 1G/10G/25G:

/interface ethernet set [ find default-name=sfp-sfpplus1] auto-negotiation=no speed=1G-baseX set [ find default-name=sfp-sfpplus1] auto-negotiation=no speed=10G-baseSR-LR set [ find default-name=sfp-sfpplus1] auto-negotiation=no speed=25G-baseSR-LR

Note: When selecting the interface speed setting, pay attention to what rates your optical module supports (check module specification data)

Note: Modules with bad EEPROM checksum do not output any EEPROM information to the ethernet monitor, which will also mean that the sfp

DDM monitor does not work for such modules.

FEC

FEC (Forward Error Correction) is a digital signal processing method that improves the bit error rate of SFP28, QSFP+, and QSFP28 links by adding information (parity bits) to the data at the transmitter side. The receiver side then uses this  information to detect and correct errors that may have been introduced during transmission.

To ensure a successful link, the same fec-mode should be used on both ends of the link. RouterOS uses a disabled fec-mode as the default setting, but it can be changed to fec74 (also known as FC-FEC) or fec91 (also known as RS-FEC). For more information on FEC mode options, refer to the property description. The table below shows link modes and supported the FEC modes:

Link Modes (for advertise and speed properties) Supported FEC modes

40G-baseSR4-LR4 fec74

40G-baseCR4 fec74

25G-baseSR-LR fec74, fec91*

|25G-baseCR|fec74, fec91*|
|---|---|
|50G-baseSR2-LR2|fec74, fec91|
|50G-baseCR2|fec74, fec91|
|100G-baseSR4-LR4|fec91|
|100G-baseCR4|fec91|
|50G-baseSR-LR|fec91 (required)|
|50G-baseCR|fec91 (required)|
|100G-baseSR2-LR2|fec91 (required)|
|100G-baseCR2|fec91 (required)|
|200G-baseSR4-LR4|fec91 (required)|
|200G-baseCR4|fec91 (required)|
|400G-baseSR8-LR8|fec91 (required)|
|400G-baseCR8|fec91 (required)|

Note: The CCR2004-1G-2XS-PCIe device does not support fec91 on SFP28 interfaces.

Description

Advertised link modes, only applies when auto-negotiation is enabled. Advertising higher speeds than the actual interface supported speed can result in undefined behavior. Multiple options are allowed.
