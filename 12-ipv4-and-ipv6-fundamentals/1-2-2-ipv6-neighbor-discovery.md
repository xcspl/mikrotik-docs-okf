---
type: Reference
title: "IPv6 Neighbor Discovery"
description: "RouterOS has IPv6 Neighbor Discovery and stateless address autoconfiguration support using Router Advertisement Daemon (RADVD)."
timestamp: '2026-05-26'
status: active
tags: [routeros, mikrotik, networking]
resource: ~/Downloads/ROS-260526-1445-796.pdf
sources:
  - resource: https://help.mikrotik.com/docs/spaces/ROS/pages/328059/RouterOS
---

# IPv6 Neighbor Discovery

Summary Node description Stateless address autoconfiguration Address states Neighbor discovery Properties Settings Prefix Properties Proxy Properties Neighbors List Examples Stateless autoconfiguration example

## Summary

Standards: RFC 2462, RFC 2461, RFC 4861

RouterOS has IPv6 Neighbor Discovery and stateless address autoconfiguration support using Router Advertisement Daemon (RADVD).

## Node description

Node is a device that implements IPv6. In IPv6 networks nodes are divided into two types:

Routers-a node that forwards IPv6 packets not explicitly addressed to itself. Hosts-any node that is not a router.

Routers and hosts are strictly separated, meaning that routers cannot be hosts and hosts cannot be routers at the same time.

## Stateless address autoconfiguration

There are several types of autoconfiguration:

stateless-address configuration is done by receiving Router Advertisement messages. These messages include stateless address prefixes and require that host is not using stateful address configuration protocol. stateful-address configuration is done by using the stateful address configuration protocol (DHCPv6). The stateful protocol is used if RA messages do not include address prefixes. both-RA messages include stateless address prefixes and require that hosts use a stateful address configuration protocol.

A highly useful feature of IPv6 is the ability to automatically configure itself without the use of a stateful configuration protocol like DHCP ( See example).

Address autoconfiguration can only be performed on multicast-capable interfaces.

It is called stateless address autoconfiguration since there is no need to manage the state on the router side. It is a very simple, robust, and effective autoconfiguration mechanism.

RouterOS uses RADVD to periodically advertise information about the link to all nodes on the same link. The information is carried by ICMPv6 "router advertisement" packet, and includes the following fields:

IPv6 subnet prefix Default router link-local address Other parameters that may be optional: are link MTU, default hop limit, and router lifetime.

Then host catches the advertisement, and configures the global IPv6 address and the default router. Global IPv6 address is generated from the advertised subnet prefix and EUI-64 interface identifier.

Optionally, the host can ask for an advertisement from the router by sending an ICMPv6 "router solicitation" packet. On Linux rtsol utility transmits the router solicitation packet. If you are running a mobile node, you may want to transmit router solicitations periodically.

### Address states

When an auto-configuration address is assigned it can be in one of the following states:

***tentative***- in this state host verifies that the address is unique. Verification occurs through duplicate address detection. ***preferred***- at this state address is verified as unique and the node can send and receive unicast traffic to and from a preferred address. The period of time of the preferred state is included in the RA message. ***deprecated***- the address is still valid, but is not used for new connections. ***invalid***- node can no longer send or receive unicast traffic. An address enters the invalid state after the valid lifetime expires.

The image above illustrates the relation between states and lifetimes.

## Neighbor discovery

Sub-menu: /ipv6 nd

In this submenu, IPv6 Neighbor Discovery (ND) protocol is configured.

Neighbor Discovery (ND) is a set of messages and processes that determine relationships between neighboring nodes. ND, compared to IPv4, replaces Address Resolution Protocol (ARP), Internet Control Message Protocol (ICMP) Router Discovery, and ICMP Redirect and provides additional functionality.

ND is used by hosts to:

Discover neighboring routers. Discover addresses, address prefixes, and other configuration parameters.

ND is used by routers to:

Advertise their presence, host configuration parameters, and on-link prefixes. Inform hosts of a better next-hop address to forward packets to a specific destination.

ND is used by nodes to:

Both resolve the link-layer address of a neighboring node to which an IPv6 packet is being forwarded and determine when the link-layer address of a neighboring node has changed. Determine whether IPv6 packets can be sent to and received from a neighbor.

RFC4861 defines five ND message types: Router Solicitation (RS), Router Advertisement (RA), Neighbor Solicitation (NS), Neighbor Advertisement (NA), and Redirect. Adding an interface to /ipv6 nd activates only the router‑side messages:

Router Solicitation (RS) – The router listens for RS sent by hosts and replies with a Router Advertisement. Router Advertisement (RA) – The router sends periodic unsolicited RAs and also responds to any RS it receives. The content of the RA (prefixes, flag bitmaps, lifetime, MTU, timer values) is taken from the per‑interface ND settings and any /ipv6 nd prefix entries. Neighbor Solicitation (NS) – The router replies with a Neighbor Advertisement when it receives an NS for any of its own addresses on that interface (link‑local, SLAAC, or static). This also covers Duplicate Address Detection (DAD) for the router's own address. Neighbor Advertisement (NA) – Sent in response to an NS (as above). Unsolicited NAs are not sent unless explicitly enabled.

Host‑to‑host NS/NA between end devices is handled automatically by the host stack and is not controlled by the ND menu. Redirect generation is optional and disabled by default (redirect=no).

Properties

|Property||Description|
|---|---|---|
|advertise-dns (yes no|| ||Option to redistribute DNS server information using RADVD. If option "yes" is selected, then RAs will include DNS|
|self; Default: no)||servers which are installed on the router itself. If option "self" is chosen, then corresponding interface link-local address will be suggested as a DNS service provider.|
|advertise-mac-address (ye s no |; Default: yes)||When set, the link-layer address of the outgoing interface is included in the RA.|
|comment (string; Default: )||Descriptive name of an item|
|dns-servers (unspecified | i pv6 addresses; Default: un specified)||Specify a single IPv6 address or list of addresses that will be provided to hosts for DNS server configuration.|
|disabled (yes no no)||; Default:|Whether an item is disabled or not. By default, entry is enabled.|
|hop-limit (unspecified|||The default value that should be placed in the Hop Count field of the IP header for outgoing (unicast) IP packets.|
|integer 0..255 [ specified)|]; Default: un||
|interface (all string Default: )||;|The interface on which to run neighbor discovery. all-run ND on all running interfaces.|
|managed-address-||The flag indicates whether hosts should use stateful autoconfiguration (DHCPv6) to obtain addresses.|
|configuration (yes no Default: no)||;||
|mtu (unspecified integer|||[The MTU option is used in router advertisement messages to ensure that all nodes on a link use the same MTU value|
|0..4294967295]; Default: u nspecified)||in those cases where the link MTU is not well known. unspecified-do not send the MTU option.|
|other-configuration (yes||| The flag indicates whether hosts should use stateful autoconfiguration to obtain additional information (excluding|
|no; Default: no)||addresses).|
|pref64-prefixes (unspecified||Specify IPv6 prefix or list of prefixes within /32, /40. /48, /56, /64, or /96 subnet that will be provided to hosts as NAT64|
|| ipv6 prefixes; Default: un specified)||prefixes.|
|ra-delay (time; Default: 3s)||The minimum time allowed between sending multicast router advertisements from the interface.|
|ra-interval (time 3s..|[|The min-max interval allowed between sending unsolicited multicast router advertisements from the interface.|
|20m50s -time 4s..30m] Default: 3m20s-10m)|[];||
|ra-preference (low   mediu|||Specify the router preference that is communicated to IPv6 hosts through router advertisements. The preference|
|m high |; Default: medium)||value in the router advertisements enables IPv6 hosts to select a default router to reach a remote destination|
|ra-lifetime (none time Default: 30m)||;|Sets the RA lifetime. A Lifetime of 0 indicates that the router is not a default router.(see Section 6.2.3 of RFC 4861)|
|reachable-time (unspecifie||The time that a node assumes a neighbor is reachable after having received a reachability confirmation. Used by the|
|d time 0..1h | [ pecified)|]; Default: uns|Neighbor Unreachability Detection algorithm (see Section 7.3 of RFC 2461)|
|retransmit-interval (unspec||The time between retransmitted Neighbor Solicitation messages. Used by address resolution and the Neighbor|
|ified | time; Default: unspe cified)||Unreachability Detection algorithm (see Sections 7.2 and 7.3 of RFC 2461)|

If ND is automatically generated by LTE configuration, then the maximum lifetime for RA will be capped at 1 hour.

Settings

Sub-menu: /ipv6 nd settings

The IPv6 ND menu has a sub-menu "Settings" which allow to change global neighbour discovery settings to be applied.

Property Description

router-advertisement-route-Specify the distance that must be used when installing SLAAC default route. distance

(integer:0..255; Default: 0)

router-advertisement-ignored-Allow to ignore specific ND received options as DNS and MTU. If RA will contain such options, they simply will be options ignored if selected on this list.

(mtu, dns; Default: )

## Prefix

Sub-menu: /ipv6 nd prefix

Prefix information sent in RA messages used by stateless address auto-configuration.

Note: The autoconfiguration process applies only to hosts and not routers.

Properties

Property Description

6to4-If this option is specified, this prefix will be combined with the IPv4 address of the interface name to produce a valid 6to4 prefix. The interface (no first 16 bits of this prefix will be replaced by 2002 and the next 32 bits of this prefix will be replaced by the IPv4 address assigned to ne | string; the interface name at configuration time. The remaining 80 bits of the prefix (including the SLA ID) will be advertised as specified in Default: ) the configuration file.

autonomous When set, indicates that this prefix can be used for autonomous address configuration. Otherwise, prefix information is silently (yes | no; ignored. Default: yes)

comment (st Descriptive name of an item ring; Default: )

disabled (ye Whether an item is disabled or not. By default, entry is enabled. s | no; Default: no)

on-link (yes When set, indicates that this prefix can be used for on-link determination. When not set the advertisement makes no statement about | no; Default: the on-link or off-link properties of the prefix. For instance, the prefix might be used for address configuration with some of the yes) addresses belonging to the prefix being on-link and others being off-link.

preferred-Timeframe (relative to the time the packet is sent) after which generated address becomes "deprecated". Deprecated is used only for lifetime (infin already existing connections and is usable until expires. valid lifetime Read more >> ity | time; Default: 1w)

prefix (ipv6 A prefix from which stateless address auto-configuration generates the valid address. If option "none" is selected, then only options prefix none | will be advertised without including specific prefix.; Default: :: /64)

valid-lifetime The length of time (relative to the time the packet is sent) an address remains in the valid state. The must be greater  valid lifetime (infinity | than or equal to the. preferred lifetime  Read more >> time; Default: 4w2d )

interface (str Interface name on which stateless auto-configuration will be running. ing; Default: )

## Proxy

Sub-menu: /ipv6 nd proxy

An ND (Neighbor Discovery) Proxy is a mechanism in IPv6 that allows a router or host to respond to Neighbor Discovery (ND) messages on behalf of another node, enabling communication across different network segments as if they were on the same link. In RouterOS proxy can be enabled per single IPv6 address and work per-interface.

Properties

Property Description

address (IPv6 address; Default:) IPv6 address which proxy will take ownership of.

comment (string; Default: ) Descriptive name of an item.

disabled (yes | no; Default: no) Whether an item is disabled or not. By default, entry is enabled.

interface (string; Default: ) Interface name on which proxy for this single IPv6 address will work.

## Neighbors List

Sub-menu: /ipv6 neighbor

|List of all discovered nodes by IPv6 neighbor discovery protocol (neighbor cache) or manually added by configuration.|||
|---|---|---|
|Property||Description|
|address (ipv6 address; Default: )||IPv6 address of the neighbour.|
|interface (string; Default: )||interface name to which this neighbour is attached.|
|mac-address (MAC; Default: 00:00:00:00:00:00)||MAC address of the device to be added.|
|Read-only Properties|||
|Property|Description||
|address (ipv6 address)|IPv6 address of the node.||
|interface (string)|The interface on which the node was detected.||
|mac-address (string)|Mac address of the discovered node.||
|router (yes | no)|Whether the discovered node is a router||

status (noarp | incomplete | Status of the cached entry: stale | reachable | delay | probe | failed) noarp-the neighbor entry is valid. No attempts to validate this entry will be made but it can be removed when its lifetime expires

incomplete-address resolution is in progress and the link-layer address of the neighbor has not yet been determined;

reachable-the neighbor is known to have been reachable recently (within tens of seconds ago);

stale-the neighbor is no longer known to be reachable but until traffic is sent to the neighbor, no attempt should be made to verify its reachability;

delay-the neighbor is no longer known to be reachable, and traffic has recently been sent to the neighbor, probes are delayed for a short period in order to give upper layer protocol a chance to provide reachability confirmation;

probe-the neighbor is no longer known to be reachable, and unicast Neighbor Solicitation probes are being sent to verify reachability. failed - the router was unable to resolve the neighbor’s MAC address using neighbor discovery protocol.

VRF (string) Indicates which VRF this neighbor entry is associated with.

The default maximum number of neighbor entries depends on the installed amount of RAM. It can be adjusted with the command "/ipv6 settings set max-neighbor-entries=x", see more details on IPv6 Settings.

## Examples

Stateless autoconfiguration example

[admin@MikroTik] > ipv6 address print Flags: X-disabled, I-invalid, D-dynamic, G-global, L-link-local # ADDRESS INTERFACE ADVERTISE 0 G 2001:db8::1/64 ether1 yes

As an example, the advertise flag is enabled which indicates that dynamic/ipv6 nd prefixentry is added.

[admin@MikroTik] > ipv6 nd prefix print Flags: X-disabled, I-invalid, D-dynamic 0 D prefix=2001:db8::/64 interface=ether1 on-link=yes autonomous=yes valid-lifetime=4w2d preferred-lifetime=1w

On a host that is directly attached to the router, we see that an address was added. The address consists of the prefix part (first 64 bits) that takes the prefix from the prefix advertisement, and the host part (last 64 bits) that is automatically generated from the local MAC address:

atis@atis-desktop:~$ ip -6 addr 1: lo: <LOOPBACK,UP,LOWER_UP> mtu 16436 inet6 ::1/128 scope host valid_lft forever preferred_lft forever 2: eth0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qlen 1000 inet6 2001:db8::21a:4dff:fe56:1f4d/64 scope global dynamic valid_lft 2588363sec preferred_lft 601163sec inet6 fe80::21a:4dff:fe56:1f4d/64 scope link valid_lft forever preferred_lft forever

The host has received the 2001:db8::/64 prefix from the router and configured an address with it.

There is also an option to redistribute DNS server information using RADVD:

[admin@MikroTik] > ip dns set server=2001:db8::2 [admin@MikroTik] > ip dns print servers: 2001:db8::2 ... [admin@MikroTik] > ipv6 nd set [f] advertise-dns=yes

You will need a running client-side software with Router Advertisement DNS support to take advantage of the advertised DNS information.

On Ubuntu/Debian Linux distributions you can install rdnssd package which is capable of receiving the advertised DNS addresses.

mrz@bumba:/$ sudo apt-get install rdnssd

mrz@bumba:/$ cat /etc/resolv.conf # Dynamic resolv.conf(5) file for glibc resolver(3) generated by resolvconf(8) # DO NOT EDIT THIS FILE BY HAND -- YOUR CHANGES WILL BE OVERWRITTEN nameserver 2001:db8::2

mrz@bumba:/$ ping6 www.mikrotik.com PING www.mikrotik.com(2a02:610:7501:1000::2) 56 data bytes 64 bytes from 2a02:610:7501:1000::2: icmp_seq=1 ttl=61 time=2.11 ms 64 bytes from 2a02:610:7501:1000::2: icmp_seq=2 ttl=61 time=1.33 ms ^C --- www.mikrotik.com ping statistics --- 2 packets transmitted, 2 received, 0% packet loss, time 1001ms rtt min/avg/max/mdev = 1.334/1.725/2.117/0.393 ms mrz@bumba:/$
