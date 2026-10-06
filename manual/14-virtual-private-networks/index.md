# Virtual Private Networks

* [Virtual Private Networks](virtual-private-networks.md) - VPN documentation provides comprehensive guides for configuring secure and encapsulated connectivity using RouterOS tunnel technologies such as IPsec, L2TP, PPTP, OpenVPN, WireGuard, and others
* [6to4](6to4.md) - This page documents the MikroTik RouterOS 6to4 interface configuration, explaining how IPv6 packets can be transmitted over IPv4 networks without explicit tunneling. It details properties like MTU, keepalive
* [EoIP](eoip.md) - Ethernet over IP (EoIP) Tunneling in MikroTik RouterOS creates secure Layer 2 bridges over IP networks using GRE encapsulation, supporting flexible topologies like LAN extension and encrypted connections with IPsec
* [GRE](gre.md) - Generic Routing Encapsulation (GRE) is a tunneling protocol for encapsulating various network protocols over IP, implemented as virtual interfaces in RouterOS with optional keepalive and properties like MTU, MSS
* [IPIP](ipip.md) - IPIP (IP-in-IP) is a tunneling protocol in RouterOS for secure point-to-point connections over IP networks, supporting IPv4 encapsulation and interoperability with other platforms. It offers basic configuration

## IPsec

* [IPsec](ipsec.md) - This section covers IPsec examples and integrations. Use it to configure IKEv2, pre-shared-key and post-quantum key workflows, and third-party VPN connectivity
* [IKEv2 EAP between NordVPN and RouterOS](ikev2-eap-between-nordvpn-and-routeros.md) - This page guides users through configuring an IKEv2 secured tunnel to NordVPN servers using EAP authentication in RouterOS v6.45+, covering root CA installation, server hostname lookup, IPsec tunnel setup with Phase
* [QKD Integration in RouterOS IPsec (PPK)](qkd-integration-in-routeros-ipsec-ppk.md) - This page introduces RouterOS IPsec's Post-Quantum Pre-shared Key (PPK) feature, detailing its integration with Quantum Key Distribution (QKD), supported key sources (static, PSK, QKD), security recommendations, and

## L2TP

* [L2TP](l2tp.md) - This page documents MikroTik RouterOS L2TP configuration, covering client and server setup with properties like authentication methods, MTU/MRRU settings, IPsec integration, and dynamic interface management for Layer
* [LAC and LNS setup with Cisco as LAC](lac-and-lns-setup-with-cisco-as-lac.md) - This page explains how to configure a MikroTik RouterOS device as an L2TP Network Server (LNS) to establish VPDN connections with a Cisco router acting as an LAC. It includes basic configuration examples for PPPoE
* [OpenVPN](openvpn.md) - OpenVPN is a secure VPN protocol offering Layer 2/3 tunneling, IPv4/IPv6 support, and flexible transport protocols (UDP/TCP). It supports client-server deployments with configurable authentication, encryption

## PPPoE

* [PPPoE](pppoe.md) - PPPoE enables IPv6 prefix delegation over PPP and MLPPP across Ethernet links, supporting both client-to-server and server-to-client configurations. It operates in discovery and session phases, with LCP/CHAP
* [IPv6 PD over PPP](ipv6-pd-over-ppp.md) - This page demonstrates configuring IPv6 Prefix Delegation over PPPoE in RouterOS, showing how to set up DHCPv6-PD pools on servers and clients, including interface configuration and verification of dynamic prefix
* [MLPPP over single and multiple links](mlppp-over-single-and-multiple-links.md) - MLPPP enhances PPP links by splitting and recombining data across multiple logical or physical links, increasing bandwidth without upgrading hardware. It supports both single-link (using MRRU) and multi-link
* [PPTP](pptp.md) - This page documents the PPTP (Point-to-Point Tunneling Protocol) implementation in MikroTik RouterOS, covering client and server configuration options including authentication methods, MTU/MRRU settings, and TCP port
* [SSTP](sstp.md) - SSTP provides secure remote access over HTTPS using TLS encryption, enabling VPN connections through firewalls and NAT devices. The page details SSTP client and server properties including authentication, encryption
* [WireGuard](wireguard.md) - WireGuard is a modern VPN solution offering fast, secure encryption across platforms with detailed configuration options including private/public keys, VRF routing, and peer management for establishing encrypted
* [ZeroTier](zerotier.md) - ZeroTier is a network virtualization engine for MikroTik RouterOS that enables secure, cross-network device connectivity via Ethernet virtualization and cryptographic peer-to-peer networks. It supports gaming, LAN
