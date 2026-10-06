# Wireless

* [Wireless](wireless.md) - This section introduces MikroTik RouterOS wireless configuration, covering package selection for different CPU types and frequency bands (2.4GHz, 5GHz, 60GHz), use cases for home access points and industrial links,

## Wi-Fi 6 / 7 (802.11ax/be)

* [Wi-Fi 6 / 7 (802.11ax/be)](wi-fi-6-7-80211axbe.md) - This page introduces the WiFi configuration menu in RouterOS, covering basic setup for password-protected and OWE transition mode access points. It explains configuration profiles, security settings, and includes
* [WiFi CAPsMAN](wifi-capsman.md) - WiFi CAPsMAN (Controlled Access Point system Manager) for the wifi-qcom / wifi-qcom-ac packages centralizes management of multiple WiFi access points. Covers CAP discovery, radio provisioning, datapath/forwarding
* [Configuring outdoor CPE to AP links](configuring-outdoor-cpe-to-ap-links.md) - Guide for configuring outdoor CPE-to-AP Wi-Fi links using MikroTik RouterOS's wifi-qcom package, covering frequency selection, country regulations, AP mode setup, security, and distance considerations for long-range
* [Configuring a wireless repeater](configuring-a-wireless-repeater.md) - This guide explains how to configure a wireless repeater using MikroTik RouterOS's wifi-qcom package, detailing setup steps for dual-band interfaces (2.4 GHz and 5 GHz), SSID management, security settings, and
* [Configuring standalone access point](configuring-standalone-access-point.md) - This guide provides instructions for configuring standalone access points (APs) using MikroTik RouterOS's wifi-qcom package, detailing setup steps for 2.4/5 GHz networks, antenna selection, and bridge configurations
* [Interworking for WiFi6](interworking-for-wifi6.md) - This page documents MikroTik RouterOS's Interworking for WiFi6, enabling secure network discovery and access point selection via IEEE 802.11u/Hotspot 2.0 standards. It explains configuration methods, interworking
* [Wi-Fi 5 (802.11ac)](wi-fi-5-80211ac.md) - MikroTik 802.11ac (Wi-Fi 5) ARM devices can be driven two ways: through the new /interface/wifi menu using the wifi-qcom-ac package (WPA3, fast roaming, new CAPsMAN) or through the legacy /interface/wireless menu

## 802.11 a/b/g/n

* [802.11 a/b/g/n](80211-abgn.md) - MikroTik 802.11 a/b/g/n devices use the legacy /interface/wireless menu provided by the wireless package. This section covers the wireless interface, MikroTik-proprietary protocols (Nstreme, Nv2), HWMP+ mesh,

## 802.11 a/b/g/n / CAPsMAN

* [CAPsMAN](capsman.md) - This page documents CAPsMAN (Centralized Access Point Management) in RouterOS, covering configuration of wireless controller settings including AAA authentication, RADIUS server integration, access lists for client
* [AP Controller (CAPsMAN)](ap-controller-capsman.md) - CAPsMAN (Controlled Access Point System Manager) centralizes wireless network management by allowing a RouterOS server to configure multiple access points, handling client authentication and data forwarding. It
* [CAPsMAN with VLANs](capsman-with-vlans.md) - This page explains configuring CAPsMAN with VLANs in MikroTik RouterOS, enabling centralized wireless management and VLAN tagging for different client groups. It covers Local Forwarding Mode setup, provisioning

## 802.11 a/b/g/n

* [HWMPplus mesh](hwmpplus-mesh.md) - This page documents the HWMP+ mesh protocol in MikroTik RouterOS, a layer-2 routing solution for wireless mesh networks using Hybrid Wireless Mesh Protocol. It covers interface properties, port configurations, FDB
* [Interworking Profiles](interworking-profiles.md) - This page describes MikroTik RouterOS interworking profiles for wireless networks, enabling devices to exchange information via IEEE 802.11u and Hotspot 2.0 standards. It details configuration properties like network
* [Nv2](nv2.md) - Nv2 is a MikroTik proprietary wireless protocol using TDMA for efficient media access in PtMP networks, supporting both Atheros 802.11n and legacy devices without hardware upgrades. It offers dynamic rate selection,
* [Spectral scan](spectral-scan.md) - The Spectral Scan feature in MikroTik RouterOS allows continuous monitoring and visualization of wireless spectrum activity, including interference detection across 2.4GHz and 5GHz bands using spectral snapshots with
* [VLANs on Wireless](vlans-on-wireless.md) - This page explains how to configure VLANs on MikroTik RouterOS wireless interfaces, enabling Layer2 segmentation between different Virtual APs and networks. It includes setup examples for isolating Guest and Work APs
* [Wireless Interface](wireless-interface.md) - RouterOS wireless interface supports IEEE 802.11 standards with comprehensive features including multiple modes (client, AP, bridge), encryption protocols, channel width adjustments, and advanced transmission
* [Wireless Troubleshooting](wireless-troubleshooting.md) - This page explains how to troubleshoot wireless connectivity issues in MikroTik RouterOS by enabling and analyzing detailed debug logs for client connections, disconnections, and security events like MIC failures or

## 60 GHz (W60G)

* [W60G](w60g.md) - This page documents MikroTik RouterOS W60G wireless interface configuration, covering setup for 60GHz point-to-point/multipoint links, ARP/MAC settings, encryption, and station management with detailed stats monitoring
* [Distance guide](distance-guide.md) - This page provides a distance guide for Point To Multi Point applications using MikroTik devices, specifying required license levels and listing compatible products such as Cube-60ad, LHG-60ad, and wAPG-60ad-A
* [Fail-over PtMP CLI example](fail-over-ptmp-cli-example.md) - This page provides a step-by-step CLI guide for configuring automatic failover between 60Ghz and 5Ghz wireless links using MikroTik RouterOS, including bridge setup, interface bonding, and W60G device connection
* [Fail-over PtP CLI example](fail-over-ptp-cli-example.md) - This page provides a step-by-step CLI example for configuring automatic failover between 60Ghz and 5Ghz wireless links using bonding, including bridge setup and W60G interface configuration for both bridge and
* [Fail-over PtP GUI example](fail-over-ptp-gui-example.md) - This guide demonstrates configuring automatic failover between a 60GHz wireless bridge and a bonded 5GHz interface using MikroTik RouterOS GUI, including bridge setup, wireless mode selection, and security profile
* [PtP CLI example](ptp-cli-example.md) - This page provides a step-by-step CLI example for configuring a transparent wireless bridge between two MikroTik W60G devices, including connecting via MAC-Telnet, setting up a bridge with interface members, and
* [PtP GUI example](ptp-gui-example.md) - This guide demonstrates configuring a transparent wireless bridge between two MikroTik W60G devices using WinBox, covering interface setup, bridge creation, wireless mode configuration for both bridge and station

## User Guides

* [Case studies](case-studies.md) - Cross-driver wireless case studies for MikroTik RouterOS: practical designs and workflows that apply to both the /interface/wireless and /interface/wifi menus, covering wireless station modes and enterprise wireless
* [Enterprise wireless security with User Manager v5](enterprise-wireless-security-with-user-manager-v5.md) - This guide explains how to configure MikroTik RouterOS User Manager v5 as an authentication server for enterprise wireless networks, covering installation, TLS certificate generation for secure EAP methods like PEAP
* [Wireless Station Modes](wireless-station-modes.md) - This page describes MikroTik RouterOS wireless station modes, explaining their differences in L2 address handling and suitability for bridging. It covers standard station mode, station-wds for WDS connections, and
