---
type: Reference
title: "Routing Protocol Reference"
description: "addresses This config entry will only apply to BFD sessions established with these specific remote neighbors."
timestamp: '2026-05-26'
status: active
tags: [routeros, mikrotik, networking]
resource: ~/Downloads/ROS-260526-1445-796.pdf
sources:
  - resource: https://help.mikrotik.com/docs/spaces/ROS/pages/328059/RouterOS
---

# Routing Protocol Reference

In This Section:

/routing/bfd

/routing/bfd/configuration /routing/bfd/session

/routing/bfd/configuration

Property Description

address-Firewall address list name. BFD configuration will apply if remote IP address is contained within specified list. list

addresses This config entry will only apply to BFD sessions established with these specific remote neighbors.

comment description string.

forbid-bfd Boolean yes / no parameter; if = yes : BFD sessions matching criteria will be prohibited.

interfaces list if interfaces where BFD configuration should be active.

min-rx Minimum receive interval, that the local router requires between received BFD packets.

min-tx Desired transmit interval, that the local router would like to use when sending BFD packets to the neighbor.

multiplier This value is multiplied by the negotiated transmission interval to determine the Hold Time; If no packets within the Hold time are received-the neighbor is declared down. Hold Time = negotiated interval × multiplier

vrf The Virtual Routing and Forwarding instance to which this configuration applies.

/routing/bfd/session

Read-only Property Description

actual-tx-interval real-time frequency at which the device currently sends BFD control packets.

/routing/bgp

/routing/bgp/instance /routing/bgp/connection /routing/bgp/template /routing/bgp/session /routing/bgp/vpls /routing/bgp/vpn /routing bgp evpn

/routing/bgp/instance

Property Description

as (integer 32-bit BGP autonomous system number. Value can be entered in AS-Plain and AS-Dot formats. The parameter is also used to set [0.. up the BGP confederation, in the following format: *confederation_as/as*. For example, if your AS is 34 and your confederation 4294967295] AS is 43, then as configuration should be as=43/34.; Default: )

cluster-id (IP In case this instance is a route reflector: the cluster ID of the router reflector cluster to this instance belongs. This attribute helps to address; recognize routing updates that come from another route reflector in this cluster and avoid routing information looping. Note that Default: ) normally there is only one route reflector in a cluster; in this case, 'cluster-id' does not need to be configured and BGP router ID is used instead

ignore-as-Whether to ignore AS_PATH attribute in the BGP route selection algorithm. Works on input. the path-len (yes | no; Default: no)

multipath (int BGP will pick configured amount of routes with similar attributes and install ECMP routes. eger [0.. 4294967295]; Default: )

router-id (IP BGP Router ID to be used. Use the ID from the /routing/router-id configuration by specifying the reference name, or set the ID | name; directly by specifying IP. Default: main ) Equal router-ids are also used to group peers into one instance.

routing-table ( Name of the routing table, to install routes in. string; Default: )

vrf (name; Name of the VRF BGP connections operates on. By default always use the "main" routing table. Default: main )

/routing/bgp/connection

A list of all connection-specific parameters can be seen in the table below.

In addition to connection-specific parameters, template-specific parameters are also directly exposed in this menu, for easier configuration in simple scenarios (when templates are not necessary).

Property Description

name (string; Default: ) Name of the BGP connection

connect (yes | no; Default: yes) Whether to allow the router to initiate the connection.

listen (yes | no; Default: yes) Whether to listen for incoming connections.

If remote.address is a host address and listening is enabled, then close the listening socket right after the first successful "accept". If remote.address is a subnet and listening is enabled, then listening socket stays open after first successful "accept" and there is a hard coded limit that allows 256 open connections.

local-a group of parameters associated with the local side of the connection

.address (IPv4/6; Default: ::) Local connection address.

.port(integer [0..65535]; Default:179 ) Local connection port.

.role(ebgp | ebgp-customer | ebgp-peer | BGP role, in most common scenarios it should be set to iBGP or eBGP. More information on BGP ebgp-provider | ebgp-rs | ebgp-rs-client | ibgp roles can be found in the corresponding RFC draft https://datatracker.ietf.org/doc/draft-ietf-idr-bgp- | ibgp-rr; Default: ) open-policy/?include_text=1)

.ttl (integer [1..255]; Default:) Time To Live (hop limit) that will be recorded in sent TCP packets.

remote-a group of parameters associated with the remote side of the connection

.address (IPv4/6; Default: ::) Remote address used to connect and/or listen to.

.port(integer [0..65535]; Default:179 ) Local connection port.

.as(integer []; Default: ) Remote AS number. If not specified BGP will determine remote AS automatically from the OPEN message.

.allowed-as(name) Name of the num-list containing remote AS numbers that will be allowed to connect. Useful for dynamic peer configuration.

.ttl (integer [1..255]; Default:) Acceptable minimum Time To Live, the hop limit for this TCP connection. For example, if 'ttl=255' then only single-hop neighbors will be able to establish the connection. This property only affects EBGP peers.

tcp-md5-key (string; Default: ) sensitive The key used to authenticate the connection with TCP MD5 signature as described in RFC 2385. If not specified, authentication is not used.

templates (name[,name]; Default: default) List of the template names, to inherit parameters from. Useful for dynamic BGP peers.

instance (name[,name]; Default: default) Name of the instance this connection is assigned to.

/routing/bgp/template

Property Description

afi (ip | ipv6 | l2vpn | l2vpn-List of address families about which this peer will exchange routing information. The remote peer must support (they cisco | vpnv4 | vpnv6 | evpn;) usually do) BGP capabilities optional parameter to negotiate any other families than IP.

as (integer [0..4294967295]; 32-bit BGP autonomous system number. Value can be entered in AS-Plain and AS-Dot formats. The parameter is also Default: ) used to set up the BGP confederation, in the following format: *confederation_as/as*. For example, if your AS is 34 and your confederation AS is 43, then as configuration should be as=43/34. Overrides instance ASN.

cisco-vpls-nlri-len-fmt (auto-VPLS NLRI length format type. Used for compatibility with Cisco VPLS. [[Read more>>]]. bits | auto-bytes | bits | bytes; Default: )

disabled (yes | no; Default: no) Whether the template is disabled.

hold-time (time[3s..1h] | Specifies the BGP Hold Time value to use when negotiating with peers. infinity; Default: 3m) According to the BGP specification, if the router does not receive successive KEEPALIVE and/or UPDATE and/or NOTI FICATION messages within the period specified in the Hold Time field of the OPEN message, then the BGP connection to the peer will be closed.

The minimal hold-time value of both peers will be used (note that the special value 0 or 'infinity' is lower than any other value)

infinity-never expire the connection and never send keepalive messages.

input-a group of parameters associated with BGP input

.accept-comunities (string A quick way to filter incoming updates with specific communities. It allows filtering incoming messages directly before; Default: ) they are even parsed and stored in memory, that way significantly reducing memory usage. Regular input filter chain can only reject prefixes which means that it will still eat memory and will be visible in /routing route table as "not active, filtered". Changes to be applied required session refresh.

.accept-ext-communities( A quick way to filter incoming updates with specific extended communities. It allows filtering incoming messages directly string; Default: ) before they are even parsed and stored in memory, that way significantly reducing memory usage. Regular input filter chain can only reject prefixes which means that it will still eat memory and will be visible in /routing route table as "not active, filtered". Changes to be applied required session refresh.

.accept-large-comunities ( A quick way to filter incoming updates with specific large communities. It allows filtering incoming messages directly string; Default: ) before they are even parsed and stored in memory, that way significantly reducing memory usage. Regular input filter chain can only reject prefixes which means that it will still eat memory and will be visible in /routing route table as "not active, filtered". Changes to be applied required session refresh.

.accept-nlri(string; Name of the ipv4/6 address-list. A quick way to filter incoming updates with specific NLRIs. It allows filtering incoming Default: ) messages directly before they are even parsed and stored in memory, that way significantly reducing memory usage. Regular input filter chain can only reject prefixes which means that it will still eat memory and will be visible in /routing route table as "not active, filtered". Changes to be applied required session restart.

.filter-unknown(string; A quick way to filter incoming updates with specific "unknown" attributes. It allows filtering incoming messages directly Default: ) before they are even parsed and stored in memory, that way significantly reducing memory usage. Regular input filter chain can only reject prefixes which means that it will still eat memory and will be visible in /routing route table as "not active, filtered". Changes to be applied required session refresh.

.affinity(afi  | alone | Configure input multi-core processing. Read more in Routing Protocol Multi-core Support article. instance | main | remote- as | vrf; Default: alone ) alone-input and output of each session are processed in its own process, most likely the best option when there are a lot of cores and a lot of peers afi, instance, vrf, remote-as-try to run input/output of new session in process with similar parameters main-run input/output in the main process (could potentially increase performance on single-core even possibly on multi-core devices with a small amount of cores) input-run output in the same process as input (can be set only for output affinity)

.allow-as (integer [0..10]; Indicates how many times to allow your own AS number in AS-PATH, before discarding a prefix. Default: )

.filter (name; Default: ) Name of the routing filter chain to be used on input prefixes. This happens after NLRIs are processed. If the chain is not specified, then BGP by default accepts everything.

.filter-comunities (string; A quick way to filter incoming updates with specific communities. It allows filtering incoming messages directly before Default: ) they are even parsed and stored in memory, that way significantly reducing memory usage. Regular input filter chain can only reject prefixes which means that it will still eat memory and will be visible in /routing route table as "not active, filtered". Changes to be applied required session refresh.

.filter-ext-communities(str A quick way to filter incoming updates with specific extended communities. It allows filtering incoming messages directly ing; Default: ) before they are even parsed and stored in memory, that way significantly reducing memory usage. Regular input filter chain can only reject prefixes which means that it will still eat memory and will be visible in /routing route table as "not active, filtered". Changes to be applied required session refresh.

.filter-large-comunities (st A quick way to filter incoming updates with specific large communities. It allows filtering incoming messages directly ring; Default: ) before they are even parsed and stored in memory, that way significantly reducing memory usage. Regular input filter chain can only reject prefixes which means that it will still eat memory and will be visible in /routing route table as "not active, filtered". Changes to be applied required session refresh.

.filter-nlri(string; Default: ) Name of the filter chain that will filter incoming IPv4/IPv6 NLRIs directly before they are  stored in memory, that way significantly reducing memory usage. Regular input filter chain can only reject prefixes which means that it will still eat memory and will be visible in /routing route table as "not active, filtered". Changes to be applied required session restart.

.filter-unknown(string; A quick way to filter incoming updates with specific "unknown" attributes. It allows filtering incoming messages directly Default: ) before they are even parsed and stored in memory, that way significantly reducing memory usage. Regular input filter chain can only reject prefixes which means that it will still eat memory and will be visible in /routing route table as "not active, filtered". Changes to be applied required session refresh.

.limit-nlri-diversity (integer; Default: )

.limit-process-routes-Try to limit the amount of received IPv4 routes to the specified number. This number does not represent the exact ipv4 (integer; Default: ) number of routes going to be installed in the routing table by the peer. BGP session "clear" command must be used to reset the flag if the limit is reached.

.limit-process-routes-Try to limit the amount of received IPv6 routes to the specified number. This number does not represent the exact ipv6 (integer; Default: ) number of routes going to be installed in the routing table by the peer. BGP session "clear" command must be used to reset the flag if the limit is reached.

.add-path (ip | ipv6) Parameter defines for which address families to accept advertised additional paths (RFC7911). Maximum path count to single destination is limited to 16 paths.

keepalive-time (time [1s.. The interval between keepalive messages, if not set by default keepalive is 1/3 of the hold-time. 30m]; Default: )

multihop (yes | no; Default: no Specifies whether the remote peer is more than one hop away. ) This option affects outgoing next-hop selection as described in RFC 4271 (for EBGP only, excluding EBGP peers local to the confederation).

It also affects:

whether to accept connections from peers that are not in the same network (the remote address of the connection is used for this check); whether to accept incoming routes with NEXT_HOP attribute that is not in the same network as the address used to establish the connection; the target-scope of the routes installed from this peer; routes from multi-hop or IBGP peers resolve their next-hops through IGP routes by default.

name (string; Default: ) Name of the BGP template

nexthop-choice (default | Affects the outgoing NEXT_HOP attribute selection. Note that next-hops set in filters always take precedence. force-self | propagate; Default: default) default-select the next-hop as described in RFC 4271 force-self-always use a local address of the interface that is used to connect to the peer as the next-hop; propagate - try to propagate further the next-hop received; i.e. if the route has BGP NEXT_HOP attribute, then use it as the next-hop, otherwise, fall back to the default case

output-a group of parameters associated with BGP output

.as-override (yes | no; If set, then all instances of the remote peer's AS number in the BGP AS-PATH attribute are replaced with the local AS Default: no) number before sending a route update to that peer. Happens before routing filters and prepending.

.affinity(afi  | alone | Configure output multicore processing. Read more in Routing Protocol Multi-core Support article. instance | main | remote- as | vrf; Default: ) alone-input and output of each session is processed in its own process, the most likely best option when there are a lot of cores and a lot of peers afi, instance, vrf, remote-as-try to run input/output of new session in process with similar parameters main-run input/output in the main process (could potentially increase performance on single-core even possibly on multicore devices with small amount of cores) input-run output in the same process as input (can be set only for output affinity)

.default-originate (always Specifies default route (0.0.0.0/0) distribution method. | if-installed | never; Default: never)

default-prepend (integer [0..255]; Default: )

.filter-chain (name; Name of the routing filter chain to be used on the output prefixes. If the chain is not specified, then BGP by default Default: ) accepts everything.

.filter-select (name; Name of the routing select chain to be used for prefix selection. If not specified, then default selection is used. Default: )

.keep-sent-attributes (yes Store in memory sent prefix attributes, required for "dump-saved-advertisements" command to work. By default, | no; Default: no) sent-out prefixes are not stored to preserve the router's memory. An option should be enabled only for debugging purposes when necessary to see currently advertised prefixes.

.network(name; Default: ) Name of the address list used to send local networks. The network is sent only if a matching IGP route exists in the routing table.

.network-blackhole (yes | If set to "yes", blackhole route will be added in the RIB for each network from the list. no)

.no-client-to-client-Disable client-to-client route reflection in Route Reflector setups. reflection (yes | no; Default: )

.no-early-cut (yes | no; The early cut is the mechanism, to guess (based on default RFC behavior) what would happen with the sent NPLRI Default: ) when received by the remote peer. If the algorithm determines that the NLRI is going to be dropped, a peer will not even try to send it. However such behavior may not be desired in specific scenarios, then then this option should be used to disable the early cut feature.

redistribute (bgp, Enable redistribution of specified route types. connected, bgp-mpls- vpn, dhcp, fantasy, modem, ospf, rip, static, vpn; Default:)

.add-path (ip | ipv6) Parameter defines for which address families select additional paths to be advertised (RFC7911). Selection of paths can be controlled with routing select chain (output.filter-select).

remove-private-as (yes | no; If set, then the BGP AS-PATH attribute is removed before sending out route updates if the attribute contains only Default: no private AS numbers.

The removal process happens before routing filters are applied and before the local, AS number is prepended to the AS path.

routing-table (string; Default: ) Name of the routing table, to install routes in. Overrides instance parameter.

save-to (string; Default: ) Filename to be used to save BGP protocol-specific packet content (Exported PDU) into pcap file. This method allows much simpler peer-specific packet capturing for debugging purposes. Pcap files in this format can also be loaded to create virtual BGP peers to recreate conditions that happened at the time when packet capture was running.

templates (name[,name]; List of template names from which to inherit parameters. Useful feature, to easily configure groups with overlapping Default: ) configuration options.

use-bfd (yes | no; Default: no) Whether to use the BFD protocol for faster connection state detection.

vrf (name; Default: main ) Name of the VRF BGP connections operates on. By default always use the "main" routing table. Overrides instance parameter.

/routing/bgp/session

Read-only Property Description

name

Also, in this menu is located a session-specific set of commands.

Command Description

clear Clear the session flags. For example, to be able to re-establish a session after the prefix limit is reached "limit-exceeded" flag must be cleared. It can be done by specifying "flag" parameter, which is able to take the following values:

input-last-notification limit-exceeded output-last-notification refused-cap-opt stopped

dump-saved-Dump saved advertisements from specified BGP session in the *.pcap file. The filename to store data is set by "save-to" parameter. advertisements

refresh Send route refresh to a specified BGP session. Is used to trigger re-sending all the routes from the remote peer. "address-family" parameters allow specifying for which address family to send route refresh.

resend Resend prefixes to a specified BGP session. The command takes two parameters:

"address-family" - parameters allow specifying for which address family to resend prefixes. "save-to" - the name of the pcap file where to dump resent messages, can be used for debugging purposes.

reset Reset specified BGP session.

stop Stop specified BGP session.

/routing/bgp/vpls

This menu lists all the configured BGP-based VPLS instances. These instances allow the router to advertise VPLS BGP NLRI and indicate that the router belongs to a specific customer VPLS network.

MP-BGP-based autodiscovery and signaling (RFC 4761).

Cisco VPLS BGP-based auto-discovery (draft-ietf-l2vpn-signaling-08).

Support for multiple import/export route target extended communities for BGP-based VPLS (both, RFC 4761 and draft-ietf-l2vpn-signaling-08).

Property Description

bridge (na The name of the bridge where dynamically created VPLS interfaces should be added as ports. me)

bridge- cost (integ er [0.. 42949672 95])

bridge-If set to none bridge horizon will not be used. horizon (n one | integer [0.. 42949672 95])

bridge-Used to assign port VLAN ID (pvid) for dynamically bridged interface. pvid (integ er 1..

4094)

cisco-id () Unique identifier. A parameter must be set for cisco-style VPLS signaling. In most cases this should not be used, any modern software supports RFC 4761 style signaling (see site-id parameter). Parameter is a merge of l2-router-id and RD, for example: 10.155.155.1&6550: 123

Short description of the item.

Defines whether an item is ignored or used.

The setting is used to tag BGP NLRI with one or more route targets which on the remote side is used by import-route-targets.

The setting is used to determine if BGP NLRI is related to a particular VPLS, by comparing route targets received from BGP NLRI.

Enables/disables Control Word usage. Read more in the VPLS Control Word article.

Advertised pseudowire MTU value.

The parameter is available starting from v5.16. It allows choosing advertised encapsulation in NLRI used only for comparison. It does not affect the functionality of the tunnel. See pw-type usage example >>

comment ( string)

disabled ( yes | no)

export- route- target (list of RTs)

import- route- targets (lis t of RTs)

local-pref ( integer[0.. 42949672 95])

name (stri ng; Default: )

pw- control- word (defa ult | disabled | enabled)

pw-l2mtu ( integer [32.. 65535])

pw-type (r aw- ethernet | tagged- ethernet | vpls)

rd (string) Specifies the value that gets attached to VPLS NLRI so that receiving routers can distinguish advertisements that may otherwise look the same. This implies that a unique route-distinguisher for every VPLS must be used. It is not necessary to use the same route distinguisher for some VPLS on all routers forming that VPLS as distinguisher is not used for determining if some BGP NLRI is related to a particular VPLS (Route Target attribute is used for this), but it is mandatory to have different distinguishers for different VPLSes. Accepts 3 types of formats. Read more>>

Unique site identifier. Each site must have a unique site-id. A parameter must be set for RFC 4761 style VPLS signaling.

Name of the VRF table.

site-id (int eger [0.. 65535])

vrf (name)

/routing/bgp/vpn

L3VPN VPNv4/VPNv6 instance configuration.

For Vpnv4/6 imported routes, scope and target scope values are chosen  as follows:

if it is a BGP route, then scope=40: if received from a multihop peer, then target-scope=30 if received from a non-multihop peer, then target-scope=10 else scope=20, target-scope=10

|Property|Description|
|---|---|
|disabled (yes | no)||
|export-a group of parameters associated with the vpnv4 export||
|.filter-chain (name)|The name of the routing filter chain that is used to filter prefixes before exporting.|

.filter-select(name) The name of the select filter chain that is used to select prefixes to be exported exporting.

.redistribute(bgp | connected | dhcp | fantasy | Enable redistribution of specified route types from VRF to VPNv4. modem | ospf | rip | static | vpn)

.route-targets(rt[,rt]) List of route targets added when exporting VPNv4 routes. The accepted RT format is similar to the one for Route Distinguishers.

import-a group of parameters associated with the vpnv4 import

.filter-chain (name) The name of the routing filter chain that is used to filter prefixes during import.

.route-targets(rt[,rt]) List of route targets that will be used to import VPNv4 routes. The accepted RT format is similar to the one for Route Distinguishers.

.router-id(name | ip) The router ID of the BGP instance that will be used for the BGP best path selection algorithm.

label-allocation-policy (per-prefix | per-vrf)

name

route-distinguisher (rd) Helps to distinguish between overlapping routes from multiple VRFs. Should be unique per VRF. Accepts 3 types of formats. Read more>>

vrf (name) Name of the VRF table that this VPN instance will use.

instance (name) Name of the instance this VPN is assigned to.

bgp evpn/routing

See EVPN documentation.

Property Description

name (string; Name of the entry Default: )

instance (name) BGP instance this EVPN is assigned to.

export-a group of parameters associated with the route export

.route-List of route targets that will be added to EVPN routes when exporting. targets (Iist of RTs)

import-a group of parameters associated with the route import

.route-List of route targets that will be used to import EVPN routes. targets (Iist of RTs)

rd (string) Specifies the value that gets attached to route so that receiving routers can distinguish advertisements that may otherwise look the same. Used to distinguish between tenants using overlapping IP ranges. Also can be used to simplify convergence and redundancy within Virtual Network. RDs form MLAG pairs should be unique, too.

vni (range of Range of Virtual Network Identifiers. integers[0.. 4294967295])

vrf (name)

/routing/fantasy

Fantasy menu is a fancy way to generate large amount of routes for testing purposes. Main benefits of this approach compared to script is the generation speed and simplicity. It is easy to remove all fantasy generated routes just by disabling fantasy rule.

Fantasy uses random generator from hashed route sequence number, seed and other parameters.

Property Description

comment (string)

count (integer:[0..4294967295]) How many routes to generate.

dealer-id (start-[end]:: integer: [0..4294967295])

disabled (yes | no) ID reference is not used.

dst-address(Prefix) Prefix from which route will be generated.

gateway (string)

instance-id (start-[end]:: integer: [0..4294967295])

name (string) Reference name

offset (integer:[0..4294967295]) Route sequence number offset

prefix-length (start-[end]:: intege Prefix length for generated route (can be specified as integer range). For example dst-address 192.168.0.0/16 and r:[0..4294967295] ) prefix-length 24 will generate /24 routes from 192.168.0.0/16 subnet.

priv-offset (start-[end]:: integer: [0..4294967295])

priv-size (start-[end]:: integer: [0..100000])

scope (start-[end]:: integer: [0.. Scope to be set, can be set as range 255])

seed (string) Random generator seed

target-scope (start-[end]:: intege Target scope to be set, can be set as range r: [0..255])

use-hold (yes | no)

/routing/filter

/routing/filter/rule /routing/filter/select-rule /routing/filter/num-list /routing/filter/community-list /routing/filter/community-ext-list /routing/filter/community-large-list /routing/filter/chain /routing/filter/select-chain

/routing/filter/rule

Property Description

chain (string; Default: )

comment (string )

disabled (yes | no)

rule (string)

/routing/filter/select-rule

Property Description

chain (string; Default: )

comment (string )

disabled (yes | no)

rule (string)

/routing/filter/num-list

Property Description

comment (string; Default: )

disabled (yes | no)

list (string) Reference name.

range (num range [0..18446744073709551615])

/routing/filter/community-list

Property Description

comment (string; Default: )

communities (list of communities; List of communities expressed either as well-known name or in the following format: "as:number", where each Default: ) section can be integer [0..65535].

Accepted well known names:

accept-own     graceful-shutdown  no-advertise         no-llgr         route-filter-6 accept-own-nh  internet           no-export            no-peer         route-filter-xlate-4 blackhole      llgr-stale         local-as  route-filter-4  route-filter-xlate-6

disabled (yes | no)

name (integer [string; Default: ) Reference name.

regexp (string) Regexp matcher to match communities. The community set with only the regexp parameter cannot be used to append/delete communities.

/routing/filter/community-ext-list

Property Description

comment (string; Default: )

communities (list of ext communities List of extended communities expressed as raw integer value or in the typed format: "type:value", where type; Default: ) can be:

rt-route-target soo -  site of origin

Value depends on the type, for more info on RT and SoO values ask google.

disabled (yes | no)

name (integer [string; Default: ) Reference name.

regexp (string) Regexp matcher to match communities. The community set with only the regexp parameter cannot be used to append/delete communities.

/routing/filter/community-large-list

Property Description

comment (string; Default: )

communities (list of large List of large communities expressed in following format: "admin:value1:value2", where each section can be communities; Default: ) integer [0..4294967295].

disabled (yes | no)

name (integer [string; Default: ) Reference name.

regexp (string) Regexp matcher to match communities. The community set with only the regexp parameter cannot be used to append/delete communities.

/routing/filter/chain

Dynamic list of filter rule chains that can be referenced in BGP/OSPF configuration.

Read-only Property Description

dynamic (yes | no)

inactive (yes | no)

name (string)

/routing/filter/select-chain

Dynamic list of filter select chains that can be referenced in BGP/OSPF configuration.

Read-only Property Description

dynamic (yes | no)

inactive (yes | no)

name (string)

/routing/filter/filter-wizard

Property Description

chain (name;) mandatory

action ( )

afi (ip | ipv6 | l2vpn | vpnv4 | vpnv6 | l2vpn-cisco)

bgp-as-path (string) regexp that matches BGP AS-Path attribute, see documentation for more details

/routing/gmp

Property Description

groups (IPv4 | IPv6 The multicast group address to be used by the interface, multiple group addresses are supported.; Default: )

interfaces (name; Name of the interface, multiple interfaces and interface lists are supported. Default: )

exclude (Default: ) When exclude is set, the interface expects to reject multicast data from the configured sources. When this option is not used, the interfaces will emit source specific join for the configured sources.

sources (IPv4 | The source address list used by the interface, multiple source addresses are supported. This setting has an effect when IGMPv3 IPv6; Default: ) or MLDv2 protocols are active.

/routing/id

Global Router ID election configuration. ID can be configured explicitly or set to be elected from one of the Routers IP addresses.

For each VRF table RouterOS adds dynamic ID instance, that elects the ID from one of the IP addresses belonging to a particular VRF:

[admin@rack1_b33_CCR1036] /routing/id> print Flags: D-DYNAMIC, I-INACTIVE Columns: NAME, DYNAMIC-ID, SELECT-DYNAMIC-ID, SELECT-FROM-VRF # NAME DYNAMIC-ID SELECT-D SELE 0 D main 111.111.111.2 only-vrf main

Property Description

comment (string)

disabled (yes | no) ID reference is not used.

id(IP) Parameter to explicitly set the Router ID. If ID is not explicitly specified, then it can be elected from one of the configured IP addresses on the router. See parameters select-dynamic-id and select-from-vrf.

name (string) Reference name

select-dynamic-id(any | lowest | only-States what IP addresses to use for the ID election: active | only-loopback | only-static | only- vrf) any-any address found on the router can be elected as the Router ID. lowest-pick the lowest IP address. only-active-pick an ID only from active IP addresses. only-loopback-pick an ID only from loopback addresses (loopback address is considered any non point to point /32 address). only-vrf-pick an ID only from selected VRF. Works with select-from-vrf property.

select-from-vrf (name) VRF from which to select IP addresses for the ID election.

Read-only Property Description

dynamic (yes | no)

dynamic-id (IP) Currently selected ID.

inactive (yes | no) If there was a problem to get a valid ID, then item can become inactive.

|||/routing/igmp-proxy /routing/igmp-proxy /routing/igmp-proxy/interface /routing/igmp-proxy/mfc /routing/igmp-proxy||
|---|---|---|---|
||Property||Description|
||query-interval (time: 1s ..1h; Default: 2m5s) query-response- interval (time: 1s..1h; Default: 10s) quick-leave|IGMP traffic received on it will be ignored.|How often to send out IGMP Query messages over downstream interfaces. How long to wait for responses to an IGMP Query message. Specifies action on IGMP Leave message. If quick-leave is on, then an IGMP Leave message is sent upstream as soon as a leave message is received from the first client on the downstream interface. Use yes only in case there is only one subscriber behind the proxy. /routing/igmp-proxy/interface Configure what interfaces will participate as IGMP proxy interfaces on the router. If an interface is not configured as an IGMP proxy interface, then all|
||Property alternative- subnets (IP/Mask; Default:) interface (name; Default: all) threshold (intege r: 0..4294967295; Default: 1) upstream (yes | no; Default: no)||Description By default, only packets from directly attached subnets are accepted. This parameter can be used to specify a list of alternative valid packet source subnets, both for data or IGMP packets. Has an effect only on the upstream interface. Should be used when the source of multicast data often is in a different IP network. Name of the interface. Minimal TTL. Packets received with a lower TTL value are ignored The interface is called "upstream" if it's in the direction of the root of the multicast tree. An IGMP forwarding router must have exactly one upstream interface configured. The upstream interface is used to send out IGMP membership requests. It is possible to get detailed status information for each interface using the print status command. [admin@MikroTik] /routing igmp-proxy interface print status Flags: X-disabled, I-inactive, D-dynamic; U-upstream 0 U interface=ether2 threshold=1 alternative-subnets="" upstream=yes source-ip-address=192.168.10.10 rx- bytes=3018487500 rx-packets=2012325 tx-bytes=0 tx-packets=0 1 interface=ether3 threshold=1 alternative-subnets="" upstream=no querier=yes source-ip-address=192. 168.20.10 rx-bytes=0 rx-packets=0 tx-bytes=2973486000 tx-packets=1982324 2 interface=ether4 threshold=1 alternative-subnets="" upstream=no querier=yes source-ip-address=192. 168.30.10 rx-bytes=0 rx-packets=0 tx-bytes=152019000 tx-packets=101346|
||Read-only Property||Description|

querier (read-only; yes|no) Whether the interface is acting as an IGMP querier.

source-ip-address (read-only; IP address) The detected source IP for the interface.

rx-bytes (read-only; integer) The total amount of received multicast traffic on the interface.

rx-packet (read-only; integer) The total amount of received multicast packets on the interface.

tx-bytes (read-only; integer) The total amount of transmitted multicast traffic on the interface.

tx-packet (read-only; integer) The total amount of transmitted multicast packets on the interface.

/routing/igmp-proxy/mfc

Multicast forwarding cache (MFC) status.

Read-only Property Description

active-downstream-interfaces The packet stream is going out of the router through this interface. (read-only: name)

bytes (read-only: integer) The total amount of received multicast traffic.

packets (read-only: integer) The total amount of received multicast packets.

wrong-packets (read-only: The total amount of received multicast packets that arrived on a wrong interface, for example, a multicast stream that is integer) received on a downstream interface instead of an upstream interface.

RouterOS support static multicast forwarding rules for IGMP proxy. If a static rule is added, all dynamic rules for that group will be ignored. These rules will take effect only if IGMP-proxy interfaces are configured (upstream and downstream interfaces should be set) or these rules won't be active.

Property Description

downstream-interfaces (name; Default: ) The received stream will be sent out to the listed interfaces only.

group (IP address) multicast group address this rule applies.The

source (IP address) The multicast data originator address.

upstream-interface ( name) interface that is receiving stream data.The

/routing/isis

/routing/nexthop

/routing/ospf

/routing/ospf/instance /routing/ospf/area /routing/ospf/area/range /routing/ospf/interface /routing/ospf/interface-template /routing/ospf/lsa /routing/ospf/neighbor /routing/ospf/static-neighbor

/routing/ospf/instance

Property Description

domain-id (Hex | MPLS-related parameter. Identifies the OSPF domain of the instance. This value is attached to OSPF routes redistributed in Address) BGP as VPNv4 routes as BGP extended community attribute and used when BGP VPNv4 routes are redistributed back to OSPF to determine whether to generate inter-area or AS-external LSA for that route. By default Null domain-id is used, as described in RFC 4577.

domain-tag (integer if set, then used in route redistribution (as route-tag in all external LSAs generated by this router), and in route calculation (all [0..4294967295]) external LSAs having this route tag are ignored). Needed for interoperability with older Cisco systems. By default not set.

in-filter (string) name of the routing filter chain used for incoming prefixes

mpls-te-address (string the area used for MPLS traffic engineering. TE Opaque LSAs are generated in this area. No more than one OSPF instance ) can have mpls-te-area configured.

mpls-te-area (string) the area used for MPLS traffic engineering. TE Opaque LSAs are generated in this area. No more than one OSPF instance can have mpls-te-area configured.

originate-default (alwa Specifies default route (0.0.0.0/0) distribution method. ys | if-installed | never; )

out-filter-chain (name) name of the routing filter chain used for outgoing prefixes filtering. Output operates only with "external" routes.

out-filter-select (name) name of the routing filter select chain, used for output selection. Output operates only with "external" routes.

redistribute (bgp, Enable redistribution of specific route types. connected,copy,dhcp, fantasy,modem,ospf, rip,static,vpn; )

router-id (IP | name; OSPF Router ID. Can be set explicitly as an IP address, or as the name of the router-id instance. Default: main)

version (2 | 3; Default: 2 OSPF version this instance will be running (v2 for IPv4, v3 for IPv6). )

vrf (name of a routing the VRF table this OSPF instance operates on table; Default: main)

use-dn (yes | no) Forces to use or ignore DN bit. Useful in some CE PE scenarios to inject intra-area routes into VRF. If a parameter is unset then the DN bit is used according to RFC. Available since v6rc12.

/routing/ospf/area

Property Description

area-id (IP OSPF area identifier. If the router has networks in more than one area, then an area with area-id=0.0.0.0 (the backbone) must always be address; present. The backbone always contains all area border routers. The backbone is responsible for distributing routing information between Default: 0. non-backbone areas. The backbone must be contiguous, i.e. there must be no disconnected segments. However, area border routers do

0.0.0) not need to be physically connected to the backbone-connection to it may be simulated using a virtual link. default-Default cost of injected LSAs into the area. If the value is not set, then stub area type-3 default LSA will not be originated. cost (integ er; unset) instance ( Name of the OSPF instance this area belongs to. name; ma ndatory) no-Flag parameter, if set then the area will not flood summary LSAs in the stub area. summaries () name (stri the name of the area ng) nssa-The parameter indicates which ABR will be used as a translator from type7 to type5 LSA. Applicable only if area type is NSSA translate ( yes | no | yes-the router will be always used as a translator candidate) no-the router will never be used as a translator
candidate-OSPF elects one of the candidate routers to be a translator

type (defa The area type. Read more on the area types in the OSPF case studies. ult | nssa | stub; Default: d efault)

/routing/ospf/area/range

Property Description

advertise (yes | no; Default: yes) Whether to create a summary LSA and advertise it to the adjacent areas.

area (name; mandatory) the OSPF area associated with this range

cost (integer [0..4294967295]) the cost of the summary LSA this range will create default - use the largest cost of all routes used (i.e. routes that fall within this range)

prefix (IP prefix; mandatory) the network prefix of this range

/routing/ospf/interface

Read-only matched interface menu

/routing/ospf/interface-template

The interface template defines common network and interface matches and what parameters to assign to a matched interface.

Matchers

Property Description

interfaces ( Interfaces to match. Accepts specific interface names or the name of the interface list. name)

network (I the network prefix associated with the area. OSPF will be enabled on all interfaces that have at least one address falling within this range. P prefix) Note that the network prefix of the address is used for this check (i.e. not the local address). For point-to-point interfaces, this means the address of the remote endpoint.

Assigned Parameters

Property Description

area (name; mandatory) The OSPF area to which the matching interface will be associated.

auth (simple | md5 | sha1 | Specifies authentication method for OSPF protocol messages. sha256 | sha384 | sha512) simple-plain text authentication md5 - keyed Message Digest 5 authentication sha-HMAC-SHA authentication RFC5709

If the parameter is unset, then authentication is not used.

auth-id (integer) The key id is used to calculate message digest (used when MD5 or SHA authentication is enabled). The value should match all OSPF routers from the same region.

authentication-key (string) sens The authentication key to be used, should match on all the neighbors of the network segment. itive

comment(string)

cost(integer [0..65535]) Interface cost expressed as link state metric.

dead-interval (time; Default: 40s Specifies the interval after which a neighbor is declared dead. This interval is advertised in hello packets. This value ) must be the same for all routers on a specific network, otherwise, adjacency between them will not form

disabled(yes | no)

hello-interval (time; Default: 10s The interval between HELLO packets that the router sends out this interface. The smaller this interval is, the faster ) topological changes will be detected, the tradeoff is more OSPF protocol traffic. This value must be the same for all the routers on a specific network, otherwise, adjacency between them will not form.

instance-id (integer [0..255]; Default: ) 0

passive () If enabled, then do not send or receive OSPF traffic on the matching interfaces

prefix-list (name) Name of the address list containing networks that should be advertised to the v3 interface.

priority (integer: 0..255; Router's priority. Used to determine the designated router in a broadcast network. The router with the highest priority Default: 128) value takes precedence. Priority value 0 means the router is not eligible to become a designated or backup designated router at all.

ROS v7 default value is 128 (defined in RFC), and the default value in ROS v6 was 1, keep this in mind when if you had strict priorities set for DR/BDR election.

retransmit-interval (time; Time interval the lost link state advertisement will be resent. When a router sends a link state advertisement (LSA) to Default: 5s) its neighbor, the LSA is kept until the acknowledgment is received. If the acknowledgment was not received in time (see transmit-delay), the router will try to retransmit the LSA.

transmit-delay (time; Default: 1s Link-state transmit delay is the estimated time it takes to transmit a link-state update packet on the interface. )

type (broadcast | nbma | ptp | the OSPF network type on this interface. Note that if interface configuration does not exist, the default network type is ptmp | ptp-unnumbered | 'point-to-point' on PtP interfaces and 'broadcast' on all other interfaces. virtual-link; Default: broadcast) broadcast-network type suitable for Ethernet and other multicast capable link layers. Elects designated router nbma-Non-Broadcast Multiple Access. Protocol packets are sent to each neighbor's unicast address. Requires manual configuration of neighbors. Elects designated router ptp-suitable for networks that consist only of two nodes. Do not elect designated router ptmp-Point-to-Multipoint. Easier to configure than NBMA because it requires no manual configuration of a neighbor. Do not elect a designated router. This is the most robust network type and as such suitable for wireless networks, if 'broadcast' mode does not work well enough for them ptp-unnumbered-works the same as ptp, except that the remote neighbor does not have an associated IP address to a specific PTP interface. For example, in case an IP unnumbered is used on Cisco devices. virtual-link-for virtual link setups.

vlink-neighbor-id (IP) Specifies the router-id of the neighbor which should be connected over the virtual link.

vlink-transit-area (name) A non-backbone area the two routers have in common over which the virtual link will be established. Virtual links can not be established through stub areas.

/routing/ospf/lsa

List of all the LSAs currently in the LSA database.

Read-only Property Description

age (integer) How long ago (in seconds) the last update occurred

area (string) The area this LSA belongs to.

body (string)

checksum (string) LSA checksum

dynamic (yes | no)

flushing (yes | no)

id (IP) LSA record ID

instance (string) The instance name this LSA belongs to.

link (string)

link-instance-id (IP)

originator (IP) An originator of the LSA record.

self-originated (yes | no) Whether LSA originated from the router itself.

sequence (string) A number of times the LSA for a link has been updated.

type (string)

wraparound (string)

/routing/ospf/neighbor

List of currently active OSPF neighbors.

Read-only Property Description

address (IP) An IP address of the OSPF neighbor router

adjacency (time) Elapsed time since adjacency was formed

An IP address of the Backup Designated Router

An IP address of the Designated Router

area (string)

bdr (string)

comment (string)

db-summaries (integer)

dr (IP)

dynamic (yes | no)

inactive (yes | no)

instance (string)

ls-requests (integer)

ls-retransmits (integer)

priority (integer)

router-id (IP)

state (down | attempt | init | 2- way | ExStart | Exchange | Loading | full)

Priority configured on the neighbor

neighbor router's RouterID

Down-No Hello packets have been received from a neighbor. Attempt-Applies only to NBMA clouds. The state indicates that no recent information was received from a neighbor. Init-Hello packet received from the neighbor, but bidirectional communication is not established (Its own RouterID is not listed in the Hello packet). 2-way-This state indicates that bi-directional communication is established. DR and BDR elections occur during this state, routers build adjacencies based on whether the router is DR or BDR, and the link is point-to- point or a virtual link. ExStart-Routers try to establish the initial sequence number that is used for the packet information exchange. The router with a higher ID becomes the master and starts the exchange. Exchange-Routers exchange database description (DD) packets. Loading-In this state actual link state information is exchanged. Link State Request packets are sent to neighbors to request any new LSAs that were found during the Exchange state. Full-Adjacency is complete, and neighbor routers are fully adjacent. LSA information is synchronized between adjacent routers. Routers achieve the full state with their DR and BDR only, an exception is P2P links.

Total count of OSPF state changes since neighbor identification state-changes (integer)

Read-only Property Description

address (IP%iface; ma ndatory )

area (name; mandatory )

comment (string)

disabled (yes | no)

instance-id (integer [0.

.255]; Default: ) 0 poll-interval (time; Default: 2m) /routing/ospf/static-neighbor Static configuration of the OSPF neighbors. Required for non-broadcast multi-access networks.
The unicast IP address and an interface, that can be used to reach the IP of the neighbor. For example, address=1.2.3.4% ether1 indicates that a neighbor with IP 1.2.3.4 is reachable on the ether1 interface.

Name of the area the neighbor belongs to.

How often to send hello messages to the neighbors which are in a "down" state (i.e. there is no traffic from them)

/routing/pim-sm

/routing/pimsm/instance /routing/pimsm/interface-template /routing/pimsm/interface /routing/pimsm/neighbor /routing/pimsm/static-rp /routing/pimsm/uib-g /routing/pimsm/uib-sg

/routing/pimsm/instance

The instance menu defines the main PIM-SM settings. The instance is then used for all other PIM-related configurations like interface-template, static RP, and Bootstrap Router.

Property

afi (ipv4 | ipv6; Default: ipv4)

bsm-forward-back (yes | no; Default: )

crp-advertise-contained (yes | no; Default: )

name (text; Default: )

rp-hash-mask-length (integer: 0.. 4294967295; Default: 30 (IPv4), or 126 (IPv6))

rp-static-override (yes | no; Default: no)

ssm-range (IPv4 | IPv6; Default: )

switch-to-spt (yes | no; Default: y es)

switch-to-spt-bytes (integer: 0.. 4294967295; Default: 0)

switch-to-spt-interval (time; Default: )

vrf (name; Default: main)

Description

Specifies address family for PIM.

Currently not implemented.

Currently not implemented.

Name of the instance.

The hash mask allows changing how many groups to map to one of the matching RPs.

Changes the selection priority for static RP. When disabled, the bootstrap RP set has a higher priority. When enabled, static RP has a higher priority.

Currently not implemented.

Whether to switch to Shortest Path Tree (SPT) if multicast data bandwidth threshold is reached. The router will not proceed from protocol phase one (register encapsulation) to native multicast traffic flow if this option is disabled. It is recommended to enable this option.

Multicast data bandwidth threshold. Switching to Shortest Path Tree (SPT) happens if this threshold is reached in the specified time interval. If a value of 0 is configured, switching will happen immediately.

Time interval in which to account for multicast data bandwidth, used in conjunction with switch-to-spt-bytes to determine if the switching threshold is reached.

Name of the VRF.

Property Description

hello-delay ( time; Default: 5s)

hello-period (time; Default: 30s )

/routing/pimsm/interface-template

The interface template menu defines which interfaces will participate in PIM and what per-interface configuration will be used.

Randomized interval for the initial Hello message on interface startup or detecting new neighbor.

Periodic interval for Hello messages.

instance (n Name of the PIM instance this interface template belongs to. ame; Default: )

interfaces ( List of interfaces that will participate in PIM. name; Default: all)

join-prune- period (time; Default: 1m )

join-Sets the value of a Tracking (T) bit in the LAN Prune Delay option in the Hello message. When enabled, a router advertises its willingness tracking-to disable Join suppression. it is possible for upstream routers to explicitly track the join membership of individual downstream routers if support (ye Join suppression is disabled. Unless all PIM routers on a link negotiate this capability, explicit tracking and the disabling of the Join s | no; suppression mechanism are not possible. Default: yes)

override-Sets the maximum time period over which to randomize when scheduling a delayed override Join message on a network that has join interval (time suppression enabled.; Default: 2 s500ms)

priority (inte The Designated Router (DR) priority. A single Designated Router is elected on each network. The priority is used only if all neighbors ger: 0.. have advertised a priority option. Numerically largest priority is preferred. In case of a tie or if priority is not used-the numerically largest 4294967295 IP address is preferred.; Default: 1)

propagation Sets the value for a prune pending timer. It is used by upstream routers to figure out how long they should wait for a Join override -delay (time message before pruning an interface that has join suppression enabled.; Default: 5 00ms)

source- addresses ( IPv4 | IPv6; Default: )

/routing/pimsm/interface

The interface menu shows all interfaces that are currently participating in PIM and their statuses. This menu contains dynamic and read-only entries that get created by defined interface templates.

Read-only Property Description

address (IP) Shows IP address.

designated-router (yes | no)

dr (yes | no)

dynamic (yes | no)

instance (name) Name of the PIM instance this interface template belongs to.

interface (name) Show the interface name.

join-tracking (yes | no)

override-interval (time)

priority (integer: 0..4294967295)

propagation-delay (time)

/routing/pimsm/neighbor

The neighbor menu shows all detected neighbors that are running PIM and their statuses. This menu contains dynamic and read-only entries.

Read-only Property Description

address (IP) Shows the neighbor's IP address and local interface the neighbor is detected on.

designated-router (yes Shows whether the neighbor is elected as Designated Router (DR). | no)

instance (name) Name of the PIM instance this neighbor is detected on.

join-tracking (yes | no) Indicates the neighbor's value of a Tracking (T) bit in the LAN Prune Delay option in the Hello message.

override-interval (time) Indicates the neighbor's value of the override interval in the LAN Prune Delay option in the Hello message.

priority (integer: 0.. Indicates the neighbor's priority value. 4294967295)

propagation-delay (time) Indicates the neighbor's value of the propagation delay in the LAN Prune Delay option in the Hello message.

timeout (time) Shows the reminding time after the neighbor is removed from the list if no new Hello message is received. The hold time equals to neighbor's hello-period * 3.5.

/routing/pimsm/static-rp

|The static-rp menu allows manually defining the multicast group to RP mappings. Such a mechanism is not robust to failures but does at least provide a||
|---|---|
|basic interoperability mechanism.||
|Property|Description|
|address (IPv4 | IPv6; Default: )|The IP address of the static RP.|
|group (IPv4 | IPv6; Default: 224.0.0.0/4)|The multicast group that belongs to a specific RP.|
|instance (name; Default: )|Name of the PIM instance this static RP belongs to.|

/routing/pimsm/uib-g

The upstream information base menus show the any-source multicast (*,G) and source-specific multicast (S,G) groups and their statuses. These menus contain only read-only entries.

Read-only Description Property

group (IPv4 | IPv6) The multicast group address.

instance (name) Name of the PIM instance the multicast group is created on.

rp (IPv4 | IPv6) The address of the Rendezvous Point for this group.

rp-local (yes | no) Indicates whether the multicast router itself is RP.

rpf (IP%interface) The Reverse Path Forwarding (RPF) indicates the router address and outgoing interface that a Join message for that group is directed to.

/routing/pimsm/uib-sg

Property Description

group (IPv The multicast group address. 4 | IPv6)

instance ( Name of the PIM instance the multicast group is created on. name)

keepalive (yes | no)

register (jo in | join- pending | prune)

rpf (IP% The Reverse Path Forwarding (RPF) indicates the router address and outgoing interface that a Join message for that group is directed to. interface)

source (IP The source IP address of the multicast group. v4 | IPv6)

spt-bit (ye The Shortest Path Tree (SPT) bit indicates whether forwarding is taking place on the (S,G) Shortest Path Tree or on the (*,G) tree. A router s | no) can have an (S,G) state and still be forwarding on a (*,G) state during the interval when the source-specific tree is being constructed. When SPT bit is false, only the (*,G) forwarding state is used to forward packets from S to G. When SPT bit is true, both (*,G) and (S,G) forwarding states are used.

/routing/rip

/routing/rip/instance /routing/rip/interface-template /routing/rip/interface /routing/rip/neighbor /routing/rip/static-neighbor /routing/rip/keys

/routing/rip/instance

|Property||Description|
|---|---|---|
|name||name of the instance|
|vrf ( Default: main)||which VRF to use|
|afi (ipv4 | ipv6; Default: )||specifies which afi to use.|
|in-filter-chain (Default: )||input filter chain|
|out-filter-chain (Default: )||output filter chain|
|out-filter-select (Default: )||output filter select rule chain|
|redistribute (bgp, bgp-mpls-vpn, connected, dhcp, fantasy, modem, ospf, rip, static, vpn; Default: )||which routes to redistribute|
|originate-default ( Default:)||whether to originate default route|
|routing-table ( Default: main)||in which routing table the routes will be added|
|route-timeout (Default: ) route-gc-timeout  (Default: )||route timeout|
|update-interval (time; Default: )||specifies time interval after which the route is considered invalid|

Note: The maximum metric of RIP route is 15. Metric higher than 15 is considered 'infinity' and routes with such metric are considered unreachable. Thus

RIP cannot be used on networks with more than 15 hops between any two routers, and using redistribute metrics larger that 1 further reduces this maximum hop count.

/routing/rip/interface-template

Property Description

name name of the instance

instance which VRF to use

interfaces specifies which afi to use.

source-addresses input filter chain

cost (Default: ) output filter chain

split-horizon (no| yes )

poison-reverse (no| yes )

mode (passive| strict)

key-chain (name) Name of key-chain which contains MD5 key. Should be set only when MD5 authentication is needed.

password sensitive Password for plain text authentication. Should be set only when plain-text authentication is needed.

/routing/rip/interface

Read-only Property Description

address (address) IP address.

instance (name) Name of the instance.

interface (name) Name of the interface.

/routing/rip/neighbor

This submenu is used to define a neighboring routers to exchange routing information with. Normally there is no need to add the neighbors, if multicasting is working properly within the network. If there are problems with exchanging routing information, neighbor routers can be added to the list. It will force the router to exchange the routing information with the neighbor using regular unicast packets.

Read-only Property Description

address (IP address) IP address of neighboring router

routes amount of routes

packets-total amount of all packets

packets-bad amount of bad packets

entries-bad amount of bad entries

last-update (time) time from last update

/routing/rip/static-neighbor

Property Description

instance (name) name of used instance

address (IP address) IP address of neighboring router

/routing/rip/keys

MD5 authentication key chains.

Property Description

chain (string; Default: "") chain name to place this key in.

key (string; Default: "") authentication key. Maximal length 16 characters

key-id (integer:0..255; Default: ) key identifier. This number is included in MD5 authenticated RIP messages, and determines witch key to use to check authentication for a specific message.

valid-from (date and time; Default: today's key is valid from this date and time date and time:) 00:00:00

valid-till (date and time; Default: today's key is valid until this date and time date and time: 00:00:00)

/routing/route

A read-only table that lists routes from all the address families as well as all filtered routes with all possible route attributes.

Default example output of the table with various route types:

[admin@MikroTik] /routing/route> print Flags: A-ACTIVE; c, s, a, l, y-COPY; H-HW-OFFLOADED Columns: DST-ADDRESS, GATEWAY, AFI, DISTANCE, SCOPE, TARGET-SCOPE, IMMEDIATE-GW DST-ADDRESS GATEWAY AFI D SCOPE TA IMMEDIATE-GW lH 10.0.0.0/8 ip4 0 ;;; defconf As 10.0.0.0/8 10.155.130.1 ip4 1 30 10 10.155.130.1%ether1 lH 10.155.130.0/25 ip4 0 Ac 10.155.130.0/25 ether1 ip4 0 10 ether1 aH 10.155.130.12/32 ip4 0 lH 111.13.0.0/24 ip4 0 Ac 111.13.0.0/24 ether2 ip4 0 10 ether2 aH 111.13.0.1/32 ip4 0 Ac 111.111.111.2/32 loopback@vrfTest ip4 0 10 loopback Ac 2111:4::/64 ether2 ip6 0 10 ether2 Ac fe80::%ether1/64 ether1 ip6 0 10 ether1 Ac fe80::%ether2/64 ether2 ip6 0 10 ether2 Ac fe80::%ether3/64 ether3 ip6 0 10 ether3 Ac fe80::%ether4/64 ether4 ip6 0 10 ether4 Ac 3333::2/128 loopback@vrfTest ip6 0 10 loopback Ac fe80::%loopback/64 loopback@vrfTest ip6 0 10 loopback Ay 111.111.111.2/32&65530:100 loopback@vrfTest vpn4 0 10 5 loopback Ay 3333::2/128&65530:100 loopback@vrfTest vpn6 0 10 5 loopback A H ether1 link 0 A H ether2 link 0 A H ether3 link 0 A H ether4 link 0 A H loopback link 0

Detailed example output with some BGP, OSPF, and other routes:

[admin@MikroTik] /routing/route> print detail Flags: X-disabled, F-filtered, U-unreachable, A-active; c-connect, s-static, r-rip, b-bgp, o-ospf, d-dhcp, v-vpn, m-modem, a-ldp-address, l-ldp- mapping, y-copy; H-hw-offloaded; + - ecmp, B-blackhole o afi=ip4 contribution=best-candidate dst-address=0.0.0.0/0 routing-table=main gateway=10.155.101.1%ether1 immediate-gw=10.155.101.1%ether1 distance=110 scope=20 target-scope=10 belongs-to="OSPF route" ospf.metric=2 .tag=111 .type=ext-type-1 debug.fwp-ptr=0x203425A0

Ad + afi=ip4 contribution=active dst-address=0.0.0.0/0 routing-table=main pref-src="" gateway=10.155.101.1 immediate-gw=10.155.101.1%ether1 distance=1 scope=30 target-scope=10 vrf-interface=ether1 belongs-to="DHCP route" debug.fwp-ptr=0x20342060

As + afi=ip4 contribution=active dst-address=0.0.0.0/0 routing-table=main pref-src="" gateway=10.155.101.1 immediate-gw=10.155.101.1%ether1 distance=1 scope=30 target-scope=10 belongs-to="Static route" debug.fwp-ptr=0x20342060

Fb afi=ip4 contribution=filtered dst-address=1.0.0.0/24 routing-table=main gateway=10.155.101.1 immediate- gw=10.155.101.1%ether1 distance=20 scope=40 target-scope=10 belongs-to="BGP IP routes from 10.155.101.217" rpki=valid bgp.peer-cache-id=*B000002 .aggregator="13335:172.68.180.1" .as-path="65530,100,9002,13335" .atomic- aggregate=yes .origin=igp debug.fwp-ptr=0x20342960

Read-only Description Property

active (yes | no) A flag indicates whether the route is elected as Active and eligible to be added to the FIB.

afi (ip4 | ip6 | link) Address family this route belongs to.

belongs-to (string) Descriptive info showing from where the route was received.

bgp (yes | no) A flag indicates whether this route was added by the BGP protocol.

bgp-a group of parameters associated with the BGP protocol

.as-path(string) value of the AS_PATH BGP attribute

.aggregator (strin

g) .atomic- aggregate (yes | no) .cluster-list (string ) .communities (str value of the COMMUNITIES BGP attribute ing) .ext-value of the EXTENDED_COMMUNITIES BGP attribute communities (stri ng) .igp-metric(string) value of the IGP_METRIC BGP attribute

value of the LARGE_COMMUNITIES BGP attribute

value of the LOCAL_PREF BGP attribute

value of the MED BGP attribute

The ID of the BGP session that installed the route. See /routing/bgp/session menu.

hex blob of unknown BGP attributes

A flag indicates whether it is a blackhole route

Currently used check-gateway option.

A flag indicates whether it is a connected network route.

Shows the route status contributing to the election process, e.g "filtered, active, candidate"

A flag indicates a copy of the route to be redistributed as the L3VPN route. VPNv4/6 related attributes are attached to this "copy" route.

debug-a group of debugging parameters

.large- communities (stri ng)

.local-pref (string)

.med (string)

.nexthop (string)

.origin (string)

.originator-id (stri ng)

.out-nexthop(stri ng)

.peer-cache-id (s tring)

.unknown (string)

.weight (string)

blackhole ()

check-gateway (ping | arp | bfd)

comment (string)

connect (yes | no)

contribution (string)

copy (yes | no)

create-time (string)

A flag indicates whether the route was added by the DHCP service.

A flag indicates whether the route is disabled.

Route destination.

A flag indicates whether the route is added as an Equal-Cost Multi-Path route in the FIB. Read more>>

A flag indicates whether the route was filtered by routing filters and excluded from being used as the best route.

Configured gateway, for the actually resolved gateway, see immediate-gw parameter.

Indicates whether the route is eligible to be hardware offloaded on supported hardware.

Shows actual (resolved) gateway and interface that will be used for packet forwarding. Displayed in format [ip% interface].

A flag indicates whether the route entry is an LDP address.

A flag indicates whether the route entry is the LDP mapping

dhcp (yes | no)

disabled (yes | no)

distance (integer)

dst-address (prefix)

ecmp (yes | no)

filtered (yes | no)

gateway (string)

hw-offloaded (yes | no)

immediate-gw (string)

label (integer)

ldp-address (yes | no)

ldp-mapping (yes | no)

ldp-a group of parameters associated with the LDP protocol

LDP mapped MPLS label.

Local IP address of the connected network.

A flag indicates whether the route is added by the LTE or 3g modems.

mpls-group of generic parameters associated with the MPLS

Mapped MPLS ingress label

Mapped MPLS egress label

A flag indicates whether the route was added by the OSPF routing protocol.

ospf-group of parameters associated with the OSPF protocol

.label (integer)

.peer-id ()

local-address (IP)

modem (yes | no)

.in-label ()

.labels ()

.out-label ()

nexthop-id ()

ospf (yes | no)

.metric (integer)

.type (string)

pref-src ()

received-from ()

rip (yes | no)

.metric ()

.route-tag ()

route-cost ()

routing-table ()

rpki (valid | invalid | unknown)

scope (integer)

static (yes | no)

target-scope (integer)

te-tunnel-id ()

total-cost ()

unreachable (yes | no)

update-time ()

ve-block-offset

ve-block-size

ve-id

vpn (yes | no)

vrf-interface ()

A flag indicates whether the route was added by the RIP routing protocol

Routing table this route belongs to.

Current status of the prefix from the RPKI validation process.

Scope used in the next-hop lookup process. Read more>>

A flag indicates statically added routes.

Target scope used in next-hop lookup process. Read more>>

Traffic Engineering tunnel ID

A flag indicates whether the route next-hop is unreachable.

A flag indicates whether the route was added by one of the VPN protocols (PPPoE, L2TP, SSTP, etc.)

Internal use only parameter which allows identifying to which VRF route should be added. Used by services that add routes dynamically, for example, DHCP client. Shown for debugging purposes.

rip-group of parameters associated with the RIP protocol

/routing/rpki

Property Description

address (IPv4/6) mandatory Address of the RTR server

disabled(yes | no; Default: no) Whether the item is ignored.

expire-interval (integer [600..172800]; Time interval [s] polled data is considered valid in the absence of a valid subsequent update from the Default: 7200) validator.

group (string) mandatory Name of the group a database is assigned to.

port (integer [0..65535]; Default: 323) Connection port number

preference (integer [0..4294967295]; If there are multiple RTR sources, the preference number indicates a more preferred one. A higher Default: 0) number is preferred.

If preference is not configured then lowest remote IP within a group is preferred, if IPs are equal then lowest remote port is preferred.

refresh-interval (integer [1..86400]; Time interval [s] to poll the newest data from the validator. Default: 3600)

retry-interval (integer [1..7200]; Default: Time Interval [s] to retry after the failed data poll from the validator.

600) vrf(name; Default: main) Name of the VRF table used to bind the connection to.

/routing/rule

List of all the parameters that can be used by routing rules:

Property Description

action (drop | An action to take on the matching packet: lookup | lookup- only-in-table | drop-silently drop the packet. unreachable) lookup-perform a lookup in routing tables. lookup-only-in-table-perform lookup only in the specified routing table (see table parameter). unreachable-generate ICMP unreachable message and send it back to the source.

chain (string) Name of the chain where rules in the routing decision will be located. by default "user" is used, if chain is not specified. If chain name is set the same as one of the built in routing decision names, then user created rules are added right after that routing decision. For example, if chain="mangle", then any user created rule n this chain will be located right after the "mangle" decision.

comment (string)

disabled (yes | no) The disabled rule is not used.

dst-address() The destination address of the packet to match.

interface (string) Incoming interface to match.

min-prefix (integer Routes from the routing table with specified prefix length is hidden to packets processed by routing rule. [0..4294967295])

Equivalent to Linux IP rule suppress_prefixlength. For example to suppress the default route in the routing decision set the value to 0.

routing-mark (string Match specific routing mark. )

src-address (string The source address of the packet to match. )

table (name) Name of the routing table to use for lookup.

/routing/settings

Property Description

check-gateway-ping-count (inte ger [0..65535], Default: 2)

check-gateway-ping-interval (ti me [100ms..10m], Default: 10s)

check-gateway-ping-timeout (ti me [1ms..1s], Default: 1s)

connected-in-chain (name)

dynamic-in-chain (name)

policy-rules (mangle | vrf-Defines order of routing decision rules. By default "user" is the chain where user defined /routing/rule is added. It is lookup | vrf-unreach | local | possible to add custom chains anywhere in the list. user | main | ...)

single-process (yes | no, Default When enabled all routing related processes are combined into single routing process to decrease RAM usage. When : no) disabled all routing related processes are processed separately, which can improve performance and stability in certain setups.

By default, single-process is enabled only for devices with 64 MB of RAM.

A reboot is required for this change to take effect.

/routing/stats

/routing/stats/memory /routing/stats/origin /routing/stats/pcap /routing/stats/process /routing/stats/step

/routing/stats/memory

/routing/stats/origin

/routing/stats/pcap

/routing/stats/process

This menu allows to monitor debugging information of all the routing processes.

/routing/table

Property Description

fib (flag) Flag indicating whether routes in this table will be installed in the FIB.

name (string) Name of the routing table
