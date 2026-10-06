---
type: Reference
title: "PPP AAA"
description: "The MikroTik RouterOS provides scalable Authentication, Authorization, and Accounting (AAA) functionality."
timestamp: '2026-05-26'
status: active
tags: [routeros, mikrotik, networking]
resource: ~/Downloads/ROS-260526-1445-796.pdf
sources:
  - resource: https://manual.mikrotik.com/docs/introduction/
---

# PPP AAA

Summary User Profiles User Database Active Users Remote AAA Examples Add new profile Add new user

## Summary

Sub-menu: /ppp

The MikroTik RouterOS provides scalable Authentication, Authorization, and Accounting (AAA) functionality.

Local authentication is performed using the User Database and the Profile Database. The actual configuration for the given user is composed using the respective user record from the User Database, the associated item from the Profile Database, and the item in the Profile database which is set as default for a given service the user is authenticating to. Default profile settings from the Profile database have the lowest priority while the user access record settings from the User Database have the highest priority with the only exception being particular IP addresses take precedence over IP pools in the local- address and remote-address settings, which are described later on.

Support for RADIUS authentication gives the ISP or network administrator the ability to manage PPP user access and accounting from one server throughout a large network. The MikroTik RouterOS has a RADIUS client that can authenticate for PPP, PPPoE PPTP L2TP OPVN,,,, and ISDN connections. The attributes received from the RADIUS server override the ones set in the default profile, but if some parameters are not received they are taken from the respective default profile.

## User Profiles

Sub-menu: /ppp profile

PPP profiles are used to define default values for user access records stored under /ppp secret submenu. Settings in /ppp secret User Database overrides corresponding /ppp profile settings except that single IP addresses always take precedence over IP pools when specified as local-address or remote-address parameters.

Properties

Property Description

address-list (string; Default: Address list name to which ppp assigned (on server) or received (on client) address will be added. )

remote-ipv6-prefix-reuse ( n If "remote-ipv6-prefix-pool" is specified and includes single "/64" prefix, then prefix can be used only for a single PPP o | yes; Default: no) client for RADVD configuration. When this option is set to value "yes", the same prefix can be reused between all the clients using this PPP profile.

bridge (string; Default: ) Name of the bridge  interface to which ppp interface will be added as a slave port. Both tunnel endpoints (server and client) must be in the bridge to make this work, see more details in the BCP bridging manual.

bridge-horizon (integer 0.. Used split-horizon value for the dynamically created bridge port. Can be used to prevent bridging loops and isolate traffic. 429496729; Default: ) Set the same value for a group of ports, to prevent them from sending data to ports with the same horizon value.

bridge-learning (default | no Changes MAC learning behavior on the dynamically created bridge port: | yes; Default: default) yes-enables MAC learning no-disables MAC learning default-derive this value from the interface default profile; same as yes if this is the interface default profile

bridge-path-cost (integer 1.. Used path cost for the dynamically created bridge port, used by STP/RSTP to determine the best path, used by MSTP to 200000000; Default: ) determine the best path between regions. This property has no effect when a bridge protocol-mode is set to none.

bridge-port-priority (integer

0..240; Default: ) bridge-port-vid (integer 1.. 4094; Default: )1 bridge-port-trusted ( no | yes; Default: no) change-tcp-mss (yes | no | default; Default: no) comment (string; Default: ) dhcpv6-lease-time (string; Default: ) dhcpv6-pd-pool (string; Default: ) dhcpv6-use-radius ( no | yes; Default: no) dns-server (IP; Default: ) idle-timeout (time; Default: ) incoming-filter (string; Default: ) insert-queue-before (bottom | first | queue name; Default: ) interface-list (interface list name; Default: ) local-address (IP address | pool; Default: ) name (string; Default: ) on-up (script; Default: )
Used priority for the dynamically created bridge port, used by STP/RSTP to determine the root port, used by MSTP to determine the root port between regions. This property has no effect when a bridge protocol-mode is set to none.

Used to assign PVID parameter for dynamically created interface. This property only has an effect when bridge vlan- filtering is set to yes.

Used to set dynamically created interface as DHCP trusted.

Modifies connection MSS settings (applies only for IPv4):

yes-adjust connection MSS value no-do not adjust connection MSS value default-derive this value from the interface default profile; same as no if this is the interface default profile

Profile comment

Lease time can be set starting from 7.20ab202, by default time is set to 1d.

Name of the IPv6 pool which will be used by dynamically created DHCPv6 server when client connects. Read more >>

Specifies value for "use-radius" option selected for dynamically generated DHCPv6 PD servers.

IP address of the DNS server that is supplied to PPP clients

Specifies the amount of time after which the link will be terminated if there is no activity present. Timeout is not set by default

Firewall chain name for incoming packets. The specified chain gets control of each packet coming from the client. The ppp chain should be manually added and rules with action=jump jump-target=ppp should be added to other relevant chains for this feature to work. For more information look at the examples section

Inserts new queue as the last, first, or before a specified queue

Specifies interface list to which profile interfaces will be added

Tunnel address or name of the pool from which the address is assigned to ppp interface locally

PPP profile name

Execute script on user login-event. These are available variables that are accessible for the event script:

user local-address remote-address caller-id called-id interface

The interface variable will return interface id value, not interface name.

Execute script on the user logging off. See on-up for more details

Defines whether a user is allowed to have more than one ppp session at a time

yes-a user is not allowed to have more than one ppp session at a time no-the user is allowed to have more than one ppp session at a time default-derive this value from the interface default profile; same as no if this is the interface default profile

on-down (script; Default: )

only-one (yes | no | default; Default: default)

Firewall chain name for outgoing packets. The specified chain gets control for each packet going to the client. The PPP chain should be manually added and rules with action=jump jump-target=ppp should be added to other relevant chains for this feature to work. For more information look at the Examples section.

Specifies parent queue

Specifies queue type. Starting from 7.19 it is possible to specify queue type for rx/tx separately, clients "upload" and "download". Use / to configure separate queue type, first is rx queue type, and then tx queue type.

outgoing-filter (string; Default: )

parent-queue (none queue | name; Default: )

queue-type (default | ethernet-default | wireless- default | synchronous- default |  hotspot-default | pcq-upload-default | pcq- download-default | only- hardware-queue | multi- queue-ethernet-default | default-small | custom queue type name; Default: )

rate-limit (string; Default: ) Rate limitation in form of rx-rate[/tx-rate] [rx-burst-rate[/tx-burst-rate] [rx-burst-threshold[/tx-burst-threshold] [rx-burst-time[ /tx-burst-time] [priority] [rx-rate-min[/tx-rate-min]]]] from the point of view of the router (so "rx" is client upload, and "tx" is client download). All rates are measured in bits per second, unless followed by an optional 'k' suffix (kilobits per second) or 'M' suffix (megabits per second). If tx-rate is not specified, rx-rate serves as tx-rate too. The same applies to tx-burst- rate, tx-burst-threshold and tx-burst-time. If both rx-burst-threshold and tx-burst-threshold are not specified (but burst-rate is specified), rx-rate and tx-rate are used as burst thresholds. If both rx-burst-time and tx-burst-time are not specified, 1s is used as default. Priority takes values 1..8, where 1 implies the highest priority, but 8 - the lowest. If rx-rate-min and tx- rate-min are not specified rx-rate and tx-rate values are used. The rx-rate-min and tx-rate-min values can not exceed rx- rate and tx-rate values.

Tunnel address or name of the pool from which address is assigned to remote ppp interface.

Assign a prefix from the IPv6 pool to the client and install the corresponding IPv6 route.

Maximum time the connection can stay up. By default, no time limit is set.

Specifies whether to use data compression or not.

yes-enable data compression no-disable data compression default-derive this value from the interface default profile; same as no if this is the interface default profile

This setting does not affect OVPN tunnels.

Specifies whether to use data encryption or not.

yes-enable data encryption no-disable data encryption default-derive this value from the interface default profile; same as no if this is the interface default profile require-explicitly requires encryption

This setting does not work on OVPN and SSTP tunnels.

Specifies whether to allow IPv6. By default is enabled if IPv6 package is installed.

yes-enable IPv6 support no-disable IPv6 support default-derive this value from the interface default profile; same as no if this is the interface default profile require-explicitly requires IPv6 support

remote-address (IP; Default: )

remote-ipv6-prefix-pool (stri ng | none; Default: none)

session-timeout (time; Default: )

use-compression (yes | no | default; Default: default)

use-encryption (yes | no | default | require; Default: def ault)

use-ipv6 (yes | no | default | require; Default: default)

|use-mpls (yes | no | default | require; Default: default) use-upnp (yes | no | default ; Default: default) wins-server (IP address; Default:) Notes|The two default profiles cannot be removed:|Specifies whether to allow MPLS over PPP. yes-enable MPLS support no-disable MPLS support default-derive this value from the interface default profile; same as no if this is the interface default profile require-explicitly requires MPLS support Specifies whether to allow UPnP yes-enable UPnP no-disable UPnP default-derive this value from the interface default profile; same as no if this is the interface default profile IP address of the WINS server to supply to Windows clients|
|---|---|---|
|Flags: * - default User Database Sub-menu: /ppp secret Properties|[admin@rb13] ppp profile> print change-tcp-mss=yes only-one=default change-tcp-mss=default [admin@rb13] ppp profile> only-one parameter is ignored if RADIUS authentication is used.|0 * name="default" use-compression=no use-encryption=no only-one=no 1 * name="default-encryption" use-compression=default use-encryption=yes incoming-filter and outgoing-filter arguments add dynamic jump rules to chain ppp, where the jump-target argument will be equal to incoming-filter or outgoi ng-filter argument in the profile. Therefore, chain ppp should be manually added before changing these arguments. PPP tunnels uses LCP protocol for MTU negotiation, it happens right when connection is established. Framed MTU attribute is not supported, as it is sent only after authentication with Radius. PPP User Database stores PPP user access records with PPP user profile assigned to each user.|
|Property||Description|
|caller-id (string; Default:) comment (string; Default:) disabled (yes | no; Default: no) limit-bytes-in (integer; Default:) 0 limit-bytes-out (integer; Default:) 0||For PPTP and L2TP it is the IP address a client must connect from. For PPPoE it is the MAC address (written in CAPITAL letters) a client must connect from. For ISDN it is the caller's number (that may or may not be provided by the operator) the client may dial-in from Short description of the user. Whether secret will be used. The maximum amount of bytes for a session that the client can upload. The maximum amount of bytes for a session that the client can download.|

local-address (IP address; IP address that will be set locally on ppp interface. Default: )

name (string; Default: ) Name used for authentication

password (string; Default: Password used for authentication ) sensitive

profile (string; Default: def Which user profile to use ault)

remote-address (IP; IP address that will be assigned to the remote ppp interface. Default: )

remote-ipv6-prefix (IPv6 IPv6 prefix assigned to ppp client. Prefix is added to ND prefix list enabling stateless address auto-configuration on ppp prefix; Default: ) interface.

routes (string; Default: ) Routes that appear on the server when the client is connected. The route format is: dst-address gateway metric (for example, 10.1.0.0/ 24 10.0.0.1 1). Other syntax is not acceptable since it can be represented incorrectly. Several routes may be specified and separated with commas. This parameter will be ignored for OpenVPN.

service (any | async | Specifies the services that a particular user will be able to use. isdn | l2tp | pppoe | pptp | ovpn | sstp; Default: any)

## Active Users

Sub-menu: /ppp active

This submenu allows monitoring active (connected) users.

/ppp active print command will show all currently connected users.

/ppp active print stats command will show received/sent bytes and packets

Properties

Property Description

address (IP address) The IP address the client got from the server

bytes (integer) Amount of bytes transferred through this connection. The first figure represents the amount of transmitted traffic from the router's point of view, while the second one shows the amount of received traffic.

caller-id (string) For PPTP and L2TP it is the IP address the client connected from. For PPPoE, it is the MAC address the client connected from.

encoding (string) Shows encryption and encoding (separated with '/' if asymmetric) being used in this connection

limit-bytes-in (integer) The maximum amount of bytes the user is allowed to send to the router.

limit-bytes-out (integer) The maximum amount of bytes the user is allowed to send to the client.

name (string) User name supplied at authentication stage

packets (integer/integer) Amount of packets transferred through this connection. The first figure represents the amount of transmitted traffic from the router's point of view, while the second one shows the amount of received traffic

service (async | isdn | l2tp | Type of service the user is using. pppoe | pptp | ovpn | sstp)

session-id (string) Shows unique client identifier.

uptime (time) User's uptime

## Remote AAA

Sub-menu: /ppp aaa

Settings in this submenu allows to set RADIUS accounting and authentication. Note that the RADIUS user database is consulted only if the required username is not found in the local user database.

Properties

Property Description

accounting Enable RADIUS accounting (yes | no; Default: yes )

interim-Interim-Update time interval update (ti me; Default: 0s)

use-radius Enable user authentication via RADIUS. If an entry in the local secret database is not found, then the client will be authenticated via (yes | no; RADIUS. Default: no )

enable-Enable IPv6 separate accounting. PPP service counts Layer2, IPv4 and IPv6 data all together when reporting network usage statistics to ipv6-the RADIUS server by default. If it is required to differ IPv4 and IPv6 traffic, then this option can be enabled. Prerequisites for it to work are accountin that the prefix must be assigned to the client through PPP service and also rate-limit must be provided. Dynamically created queue g (yes | no statistics will be used as counters for IPv6 data, which then will be included in accounting packets as separate IPv6 statistics attributes.; Default: This will not work for prefixes assigned by dynamically created DHCPv6 server due to provided prefix pool or PPP/Profile configuration. no) Then prefix assignment is handled by DHCP service, not PPP, thus accounting can not be managed by PPP service.

## Examples

Add new profile

To add the profile ex that assigns the router itself the 10.0.0.1 address, and the addresses from the ex pool to the clients, filtering traffic coming from clients through mypppclients chain:

[admin@rb13] ppp profile> add name=ex local-address=10.0.0.1 remote-address=ex incoming-filter=mypppclients [admin@rb13] ppp profile> print Flags: * - default 0 * name="default" use-compression=no use-vj-compression=no use-encryption=no only-one=no change-tcp-mss=yes 1 name="ex" local-address=10.0.0.1 remote-address=ex use-compression=default use-vj-compression=default use-encryption=default only-one=default change-tcp-mss=default incoming-filter=mypppclients 2 * name="default-encryption" use-compression=default use-vj-compression=default use-encryption=yes only-one=default change-tcp-mss=default [admin@rb13] ppp profile>

Add new user

To add the user ex with password lkjrht and profile ex available for PPTP service only, enter the following command:

[admin@rb13] ppp secret> add name=ex password=lkjrht service=pptp profile=ex [admin@rb13] ppp secret> print Flags: X-disabled # NAME SERVICE CALLER-ID PASSWORD PROFILE REMOTE-ADDRESS 0 ex pptp lkjrht ex 0.0.0.0 [admin@rb13] ppp secret>
