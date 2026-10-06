---
type: Reference
title: "PPPoE"
description: "PPPoE provides the ability to connect a network of hosts over a simple bridging access device to a remote Access Concentrator."
timestamp: '2026-05-26'
status: active
tags: [routeros, mikrotik, networking]
resource: ~/Downloads/ROS-260526-1445-796.pdf
sources:
  - resource: https://manual.mikrotik.com/docs/introduction/
---

# PPPoE

Overview Introduction PPPoE Operation Discovery phase Session phase MTU PPPoE Client Properties Status Scanner PPPoE Server Access concentrator Properties Quick Example PPPoE Client PPPoE Server

## Overview

Point to Point over Ethernet (PPPoE) is simply a method of encapsulating PPP packets into Ethernet frames. PPPoE is an extension of the standard Point to Point Protocol (PPP) and it the successor of PPPoA. PPPoE standard is defined in RFC 2516. The PPPoE client and server work over any Layer2 Ethernet level interface on the router, for example, Wireless, Ethernet, EoIP, etc. Generally speaking, PPPoE is used to hand out IP addresses to clients based on authentication by username (and also if required, by workstation) as opposed to workstation only authentication where static IP addresses or DHCP are used. It is advised not to use static IP addresses or DHCP on the same interfaces as PPPoE for obvious security reasons.

## Introduction

PPPoE provides the ability to connect a network of hosts over a simple bridging access device to a remote Access Concentrator.

Supported connections:

MikroTik RouterOS PPPoE client to any PPPoE server; MikroTik RouterOS server (access concentrator) to multiple PPPoE clients (clients are available for almost all operating systems and most routers);

## PPPoE Operation

PPPoE has two distinct stages(phases):

1. Discovery phase;
2. Session phase;
### Discovery phase

There are four steps to the Discovery stage. When it completes, both peers know the PPPoE SESSION_ID and the peer's Ethernet address, which together define the PPPoE session uniquely:

1.  PPPoE Active Discovery Initialization (PADI) - The PPPoE client sends out a PADI packet to the broadcast address. This packet can also populate the "service-name" field if a service name has been entered in the dial-up networking properties of the PPPoE client. If a service name has not been entered, this field is not populated
2. PPPoE Active Discovery Offer (PADO) - The PPPoE server, or Access Concentrator, should respond to the PADI with a PADO if the Access Concentrator is able to service the "service-name" field that had been listed in the PADI packet. If no "service-name" field had been listed, the Access Concentrator will respond with a PADO packet that has the "service-name" field populated with the service names that the Access Concentrator can service. The PADO packet is sent to the unicast address of the PPPoE client
3. PPPoE Active Discovery Request (PADR) - When a PADO packet is received, the PPPoE client responds with a PADR packet. This packet is sent to the unicast address of the Access Concentrator. The client may receive multiple PADO packets, but the client responds to the first valid PA

3. DO that the client received. If the initial PADI packet had a blank "service-name" field filed, the client populates the "service-name" field of the PADR packet with the first service name that had been returned in the PADO packet.
4. PPPoE Active Discovery Session Confirmation (PADS) - When the PADR is received, the Access Concentrator generates a unique session identification (ID) for the Point-to-Point Protocol (PPP) session and returns this ID to the PPPoE client in the PADS packet. This packet is sent to the unicast address of the client.
PPPoE session termination:

PPPoE Active Discovery Terminate (PADT) - Can be sent anytime after a session is established to indicate that a PPPoE session terminated. It can be sent by either server or client.

### Session phase

When the discovery stage is completed, both peers know PPPoE Session ID and other peer's Ethernet (MAC) address which together defines the PPPoE session. PPP frames are encapsulated in PPPoE session frames, which have Ethernet frame type 0x8864. When a server sends confirmation and a client receives it, PPP Session is started that consists of the following stages:

1. LCP negotiation stage
2. Authentication (CHAP/PAP) stage
3. IPCP negotiation stage-where the client is assigned an IP address. If any process fails, the LCP negotiation establishment phase is started again.
PPPoE server sends Echo-Request packets to the client to determine the state of the session, otherwise, the server will not be able to determine that session is terminated in cases when a client terminates session without sending Terminate-Request packet.

MTU

Typically, the largest Ethernet frame that can be transmitted without fragmentation is 1500 bytes. PPPoE adds another 6 bytes of overhead and the PPP field adds two more bytes, leaving 1492 bytes for IP datagram. Therefore max PPPoE MRU and MTU values must not be larger than 1492.

TCP stacks try to avoid fragmentation, so they use an MSS (Maximum Segment Size). By default, MSS is chosen as MTU of the outgoing interface minus the usual size of the TCP and IP headers (40 bytes), which results in 1460 bytes for an Ethernet interface. Unfortunately, there may be intermediate links with lower MTU which will cause fragmentation. In such a case TCP stack performs path MTU discovery. Routers that cannot forward the datagram without fragmentation are supposed to drop the packet and send ICMP-Fragmentation-Required to originating host. When a host receives such an ICMP packet, it tries to lower the MTU. This should work in the ideal world, however in the real world many routers do not generate fragmentation-required datagrams, also many firewalls drop all ICMP datagrams.

The workaround for this problem is to adjust MSS if it is too big.

## PPPoE Client

Properties

Property Description

ac-name (string; Default: ) "" Access Concentrator name, this may be left blank and the client will connect to any access concentrator on the broadcast domain

add-default-route (yes|no; Enable/Disable whether to add default route automatically Default: no)

allow (mschap2|mschap1|c allowed authentication methods, by default all methods are allowed hap|pap; Default: mschap2, mschap1,chap,pap)

default-route-distance (byte sets distance value applied to auto created default route, if add-default-route is also selected [0..255]; Default: )1

dial-on-demand (yes|no; connects to AC only when outbound traffic is generated. If selected, then route with gateway address from 10.112.112.0 Default: no) /24 network will be added while connection is not established.

interface (string; Default: ) interface name on which client will run

keepalive-timeout (integer; Sets keepalive timeout in seconds. Keepalive-timeout=disabled option is added to disable echo packages on link, this will Default:60) stop negotiation on mtu. At this point 1600 can be set. Check if server supports, most probably path mtu is blocking jumbo frames. If path of mtu allows jumbo frames, the mtu of 1600 will also work.

max-mru (integer; Default: Maximum Receive Unit

1460) max-mtu (integer; Default: Maximum Transmission Unit
1460) mrru (integer: 512..
maximum packet size that can be received on the link. If a packet is bigger than tunnel MTU, it will be split into multiple 65535|disabled; Default: di packets, allowing full size IP or Ethernet packets to be sent over the tunnel. sabled)

name (string; Default: pppo name of the PPPoE interface, generated by RouterOS if not specified e-out[i])

password (string; Default: password used to authenticate ) sensitive

profile (string; Default: defa Specifies which PPP profile configuration will be used when establishing the tunnel. ult)

service-name (string; specifies the service name set on the access concentrator, can be left blank to connect to any PPPoE server Default: ) ""

use-peer-dns (yes|no; enable/disable getting DNS settings from the peer Default: no)

user (string; Default: ) "" username used for authentication

Status

Command /interface pppoe-client monitor will display current PPPoE status.

Available read only properties:

Property Description

ac-mac (MAC address) MAC address of the access concentrator (AC) the client is connected to

ac-name (string) name of the Access Concentrator

active-links (integer) Number of bonded MLPPP connections, ('1' if not using MLPPP)

encoding (string) encryption and encoding (if asymmetric, separated with '/') being used in this connection

local-address (IP Address) IP Address allocated to client

remote-address (IP Address) Remote IP Address allocated to server (ie gateway address)

mru (integer) effective MRU of the link

mtu (integer) effective MTU of the link

service-name (string) used service name

status (string) current link status. Available values are:

dialing, verifying password..., connected, disconnected.

uptime (time) connection time displayed in days, hours, minutes and seconds

Scanner

PPPoE Scanner allows scanning all active PPPoE servers in the layer2 broadcast domain. Command to run scanner is as follows:

/interface pppoe-client scan [interface]

Available read only properties:

Property Description

service (string) Service name configured on server

mac-address (MAC) Mac address of detected server

ac-name (string) name of the Access Concentrator

For Windows, some connection instructions may use the form where the "phone number", such as "MikroTik_AC\mt1", is specified to indicate that "MikroTik_AC" is the access concentrator name and "mt1" is the service name.

Specifying MRRU means enabling MP (Multilink PPP) over a single link. This protocol is used to split big packets into smaller ones. Under Windows, it can be enabled in the Networking tab, Settings button, "Negotiate multi-link for single link connections". MRRU is hardcoded to 1614 on Windows. This setting is useful to overcome PathMTU discovery failures. The MP setting should be enabled on both peers.

## PPPoE Server

There are two types of interface (tunnel) items in PPPoE server configuration-static users and dynamic connections. An interface is created for each tunnel established to the given server. Static interfaces are added administratively if there is a need to reference the particular interface name (in firewall rules or elsewhere) created for the particular user. Dynamic interfaces are added to this list automatically whenever a user is connected and its username does not match any existing static entry (or in case the entry is active already, as there can not be two separate tunnel interfaces referenced by the same name-set one-session-per-host value if this is a problem). Dynamic interfaces appear when a user connects and disappear once the user disconnects, so it is impossible to reference the tunnel created for that use in router configuration (for example, in firewall), so if you need a persistent rule for that user, create a static entry for him/her. Otherwise, it is safe to use a dynamic configuration.

In both cases PPP users must be configured properly-static entries do not replace PPP configuration.
