---
type: Reference
title: "Access concentrator"
description: "accept-untagged (yes This setting controls whether the PPPoE server will accept untagged (non-VLAN) PPPoE packets on its interface, when ppp no; Default: yes) oe-over-vlan-range is specified."
timestamp: '2026-05-26'
status: active
tags: [routeros, mikrotik, networking]
resource: ~/Downloads/ROS-260526-1445-796.pdf
sources:
  - resource: https://help.mikrotik.com/docs/spaces/ROS/pages/328059/RouterOS
---

# Access concentrator

/interface pppoe-server server

Properties

Property Description

accept-untagged (yes | This setting controls whether the PPPoE server will accept untagged (non-VLAN) PPPoE packets on its interface, when ppp no; Default: yes) oe-over-vlan-range is specified.

By default, untagged PPPoE packets are accepted. If you are using the pppoe-over-vlan-range property (which enabled PPPoE over 802.1Q VLANs), this option lets you decide whether to still allow untagged clients on the same interface. If you are not using the pppoe-over-vlan-range, this setting do not have any effect.

Authentication algorithm. authentication ( mschap2 | mschap1 | chap | pap; Default: "mschap2, mschap1, chap, pap")

default-profile (string; Default: "default")

interface (string; Default: Interface that the clients are connected to. "")

Defines the time period (in seconds) after which the router is starting to send keepalive packets every second. If there is no keepalive-timeout (time; Default: "10", or disabled) traffic and no keepalive responses arrive for that period of time (i.e. 2 * keepalive-timeout), the non responding client is proclaimed disconnected.

After a successful LCP handshake, the client sends LCP echo packets to verify MTU forwarding; if no reply is received, it falls back to a backup MTU of 1480. A new option, keepalive-timeout=disabled, disables sending echo packets, effectively turning off the MTU test.

max-mru (integer; Default: "1480")

max-mtu (integer; Default: "1480")

max-sessions (integer; Default: "0")

mrru (integer: 512.. 65535 | disabled; Default: "disabled")

one-session-per-host (ye s | no; Default: "no")

Maximum Receive Unit. The optimal value is the MTU of the interface the tunnel is working over reduced by 20 (so, for 1500-byte Ethernet link, set the MTU to 1480 to avoid fragmentation of packets)

Maximum Transmission Unit. The optimal value is the MTU of the interface the tunnel is working over reduced by 20 (so, for 1500-byte Ethernet link, set the MTU to 1480 to avoid fragmentation of packets)

Maximum number of clients that the AC can serve. '0' = no limitations.

Maximum packet size that can be received on the link. If a packet is bigger than tunnel MTU, it will be split into multiple packets, allowing full size IP or Ethernet packets to be sent over the tunnel.

Allow only one session per host (determined by MAC address). If a host tries to establish a new session, the old one will be closed.

pppoe-over-vlan-range (i This setting allows a PPPoE server to operate over 802.1Q VLANs. By default, a PPPoE server only accepts untagged nteger 1..4094; Default: "") packets on its interface. However, in scenarios where clients are on separate VLANs, instead of creating multiple 802.1Q VLAN interfaces and bridging them together or configuring individual PPPoE servers for each VLAN, you can specify the necessary VLANs directly in the PPPoE server settings.

When you specify the VLAN IDs, the PPPoE server will accept 802.1Q tagged packets from clients, and it will reply using the same VLAN. You then have an option to accept or drop untagged PPoE clients on the same interface using the accept -untagged property.

You can configure the PPPoE server with pppoe-over-vlan-range setting even on VLAN interface enabling the QinQ setups as well. But keep in mind that the inner VLAN tag should be 802.1Q.

The setting supports a range of VLAN IDs, as well as individual VLANs specified using comma-separated values. For example: pppoe-over-vlan-range=100-115,120,122,128-130.

Avoid configuring a server with pppoe-over-vlan-range on an interface while also creating a VLAN interface using a VLAN ID that falls within that range. For example:

/interface vlan add interface=ether2 name=vlan15 vlan-id=15 /interface pppoe-server server add disabled=no interface=ether2 pppoe-over-vlan-range=10-20

If you need this type of setup, remove the overlapping VLAN ID from pppoe-over-vlan-rang and create a separate PPPoE server instance directly on the VLAN interface, like this:

/interface vlan add interface=ether2 name=vlan15 vlan-id=15 /interface pppoe-server server add disabled=no interface=ether2 pppoe-over-vlan-range=10-14,16-20 add disabled=no interface=vlan15

service-name (string; The PPPoE service name. Server will accept clients which sends PADI message with service-names that matches this Default: ) "" setting or if service-name field in PADI message is not set.

The PPPoE server (access concentrator) supports multiple servers for each interface-with differing service names. The access concentrator name and PPPoE service name are used by clients to identify the access concentrator to register with. The access concentrator name is the same as the identity of the router displayed before the command prompt. The identity may be set within the /system identity submenu.

Do not assign an IP address to the interface you will be receiving the PPPoE requests on.

Specifying MRRU means enabling MP (Multilink PPP) over a single link. This protocol is used to split big packets into smaller ones.  Their MRRU is hardcoded to 1614. This setting is useful to overcome PathMTU discovery failures. The MP setting should be enabled on both peers.

The default keepalive-timeout value of 10s is OK in most cases. If you set it to 0, the router will not disconnect clients until they explicitly log out or the router is restarted. To resolve this problem, the one-session-per-host property can be used.

## Quick Example

### PPPoE Client

To configure MikroTik RouterOS to be a PPPoE client, just add a PPPoE-client with the following parameters as in the example:

[admin@MikroTik] > interface pppoe-client add interface=ether2 password=StrongPass service-name=pppoeservice name=PPPoE-Out disabled=no user=MT-User [admin@MikroTik] > interface pppoe-client print Flags: X-disabled, I-invalid, R-running 0 R name="PPPoE-Out" max-mtu=auto max-mru=auto mrru=disabled interface=ether2 user="MT-User" password="StrongPass" profile=default keepalive-timeout=10 service-name="pppoeservice" ac-name="" add-default-route=no dial-on-demand=no use-peer-dns=no allow=pap,chap,mschap1,mschap2

### PPPoE Server

To configure MikroTik RouterOS to be an Access Concentrator (PPPoE Server):

add an IP address pool for the clients from 10.0.0.2-10.0.0.5; add PPP profile; add PPP secret (username/password); add the PPPoE server itself;

[admin@MikroTik] > /ip pool add name=pppoe-pool ranges=10.0.0.2-10.0.0.5 [admin@MikroTik] > /ppp profile add local-address=10.0.0.1 name=for-pppoe remote-address=pppoe-pool [admin@MikroTik] > /ppp secret add name=MT-User password=StrongPass profile=for-pppoe service=pppoe [admin@MikroTik] > /interface pppoe-server server add default-profile=for-pppoe disabled=no interface=ether3 service-name=pppoeservice

Notes

Its not recommended to use large amount of pppoe-clients on one device.
