---
type: Reference
title: "Quick Example"
description: "To establish an L2TP Ether tunnel, the L2TP Ether interface must be created on the client side, while the L2TP server must be enabled on the remote (server) side. Once both sides are configured correctly, a dynamic inter."
timestamp: '2026-05-26'
status: active
tags: [routeros, mikrotik, networking]
resource: ~/Downloads/ROS-260526-1445-796.pdf
sources:
  - resource: https://help.mikrotik.com/docs/spaces/ROS/pages/328059/RouterOS
---

# Quick Example

### L2TP Server

On the servers side we will enable L2TP-server and create a PPP profile for a particular user:

[admin@MikroTik] > /interface l2tp-server server set enabled=yes [admin@MikroTik] > /ppp secret add local-address=10.0.0.2 name=MT-User password=StrongPass profile=default- encryption remote-address=10.0.0.1 service=l2tp

### L2TP Client

L2TP client setup in the RouterOS is very simple.  In the following example, we already have a preconfigured 3 unit setup. We will take a look more detailed on how to set up L2TP client with username "MT-User", password "StrongPass" and server 192.168.51.3:

[admin@MikroTik] > /interface l2tp-client \ add connect-to=192.168.51.3 disabled=no name=MT-User password=StrongPass user=MT-User [admin@MikroTik] > /interface l2tp-client print Flags: X-disabled, R-running 0 R name="MT-User" max-mtu=1450 max-mru=1450 mrru=disabled connect-to=192.168.51.3 user="MT-User" password="StrongPass" profile=default-encryption keepalive-timeout=60 use-ipsec=no ipsec-secret="" allow-fast-path=no add-default-route=no dial-on-demand=no allow=pap,chap,mschap1,mschap2

## L2TP Ether Overview

Layer 2 Tunnel Protocol Version 3 (L2TPv3) is a draft from the Internet Engineering Task Force (IETF) working group. It introduces various improvements to the original L2TP, allowing the encapsulation of Layer 2 (L2) payloads within L2TP. More precisely, L2TPv3 outlines the protocol for tunnelling Layer 2 payloads across an IP core network using L2 virtual private networks (VPNs).

To establish an L2TP Ether tunnel, the L2TP Ether interface must be created on the client side, while the L2TP server must be enabled on the remote (server) side. Once both sides are configured correctly, a dynamic interface is automatically created between them, forming a transparent Layer 2 connection across the IP network.

Server Side (L2TP Server)

/interface l2tp-server server enabled=setyes

Client Side (L2TP Ether Interface)

/interface l2tp-ether add connect-to=1.1.1.1 disabled=no

Properties

Property

connect-to ( IP; Default: )

comment ( string; Default: )

disabled ( yes | no; Default: yes)

mac-address ( string; Default: auto)

unmanaged-mode ( yes | no; Default: no)

local-tunnel-id ( string; Default: disabled)

local-session-id ( string; Default: disabled)

remote-tunnel-id ( string; Default: di sabled)

remote-session-id ( string; Default: disabled)

peer-cookie ( string; Default: disabl ed)

send-cookie ( string; Default: disabled)

mtu (auto; Default: 1420)

name (string; Default: )

local-address (IP address; Default: )

use-ipsec (yes | no; Default: no)

allow-fast-path (yes | no; Default: no )

l2tp-proto-version (  l2tpv3-ip | l2tpv3-udp |; Default: l2tpv3-udp )

cookie-length ( 0 | 4-bytes | 8- bytes; Default:  ) 0

digest-hash (md5 | none | sha1; Default: md5 )

use-l2-specific-sublayer ( yes | no; Default: no)

circuit-id

ipsec-secret (string; Default: ) sensi tive

Description

Remote address of L2TP server.

Short description of the tunnel.

Enables/disables tunnel.

Set desired mac address of interface.

Set unmanaged mode active, the configuration for additional settings will be possible, such as: peer-cookie, send- cookie, local-tunnel-id, local-session-id, remote-tunnel-id, remote-session-id, local-address.

Set value for local-tunnel-id, an integer required.

Set value for local-session-id, an integer required.

Set value for remote-tunnel-id, an integer required.

Set value for remote-session-id, an integer required.

Sets optional peer cookie. To enable cookie enter remote cookie value (8 or 16 character hex string value expected) to disable leave empty.

Sets optional cookie. To enable cookie enter remote cookie value (8 or 16 character hex string value expected) to disable leave empty.

Maximum Transmission Unit. Max packet size that L2TP interface will be able to send without packet fragmentation.

Descriptive name of the interface.

Set local address for unmanaged mode.

When this option is enabled, dynamic IPSec peer configuration and policy is added to encapsulate L2TP connection into IPSec tunnel.

Allow to forward packets without additional processing in the Linux kernel.

Specify protocol version.

Configures an L2TPv3 pseudowire static session cookie.

Specifies which hash function to be used.

Specify source address.

Set the virtual circuit identifier to bind the one end of the L2TPv3 control channel, this works as identifier for each redundant pseudowire.

Preshared key used when use-ipsec is enabled.
