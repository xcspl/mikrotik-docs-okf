---
type: Reference
title: "DHCPv6 Server"
description: "Single DUID is used for client and server identification, only IAID will vary between clients corresponding to their assigned interface."
timestamp: '2026-05-26'
status: active
tags: [routeros, mikrotik, networking]
resource: ~/Downloads/ROS-260526-1445-796.pdf
sources:
  - resource: https://help.mikrotik.com/docs/spaces/ROS/pages/328059/RouterOS
---

# DHCPv6 Server

Summary

Standards: RFC 3315, RFC 3633

Single DUID is used for client and server identification, only IAID will vary between clients corresponding to their assigned interface.

Client binding creates a dynamic pool with a timeout set to binding's expiration time (note that now dynamic pools can have a timeout), which will be updated every time binding gets renewed.

When a client is bound to a prefix, the DHCP server adds routing information to know how to reach the assigned prefix.

General

Sub-menu: /ipv6 dhcp-server

This sub-menu lists and allows to configure DHCP-PD servers.

### DHCPv6 Server Properties

Property

address-pool (enum | static-only; Default: static-only)

prefix-pool (enum | static-only; Default: st atic-only)

allow-dual-stack- queue (yes | no; Default: yes)

address-lists (string; Default:)

binding-script (string; Default: )

dhcp-option (string; Default: none)

insert-queue-before ( bottom | first | name; Default: first)

parent-queue (string | none; Default: none)

preference (integer [0..255]; Default: 255)

disabled (yes | no; Default: no)

interface (string; Default: )

lease-time (time; Default: 3d)

rapid-commit (yes | no; Default: yes)

route-distance (integ er [0..255]; Default: )1

Description

IPv6 pool, from which to take IPv6 address for the clients, pool prefix-length must be specified as /128.

IPv6 pool, from which to take IPv6 prefxies for the clients.

Creates a single simple queue entry for both IPv4 and IPv6 addresses, and uses the MAC address and DUID for identification. Requires IPv6 DHCP Server to have this option enabled as well to work properly.

Comma seperated list of address-lists. Address or prefix issued by the server will be added to these lists.

A script that will be executed after binding is assigned or de-assigned. Internal "global" variables that can be used in the script:

bindingBound-set to "1" if bound, otherwise set to "0" bindingServerName-dhcp server name bindingDUID-DUID bindingAddress-active address bindingPrefix-active prefix

Add additional DHCP options from option list.

Specify where to place dynamic simple queue entries for static DHCP leases with rate-limit parameter set. a

A dynamically created queue for this lease will be configured as a child queue of the specified parent queue.

Defines server priority level in client selection when multiple servers respond.

Whether DHCP-PD server participates in the prefix assignment process.

The interface on which server will be running.

The time that a client may use the assigned address. The client will try to renew this address after half of this time and will request a new address after the time limit expires.

Enables a two-message exchange (Solicit and Reply) for quicker client configuration by skipping the standard four-message process.

Specify distance to set for dynamically installed routes towards DHCPv6 clients.

use-radius (yes | no | Whether to use RADIUS server: accounting; Default: no) no-do not use RADIUS; yes-use RADIUS for accounting and lease; accounting-use RADIUS for accounting only.

use-reconfigure (yes Allow the server to send Reconfigure messages to clients, prompting them to renew or update their configuration without waiting | no; Default: no) for their lease to expire.

name (string; Reference name Default: )

address-list (string; Address list to which address will be added if the lease is bound. Default: none)

ignore-ia-na-bindings Do not reply to DHCPv6 address requests and process only prefixes. Without this setting even if server does not have address- (yes | no; Default: no) pool configured, it has to respond to client that there is no address available for the client. That can lead up to the situation when DHCPv6 client requests address and prefix in a loop.

Read-only Properties

Property Description

dynamic (yes | no)

invalid (yes | no)

Bindings

Sub-menu: /ipv6 dhcp-server binding

DUID is used only for dynamic bindings, so if it changes then the client will receive a different prefix than previously.

Property Description

address (IPv6 IPv6 prefix that will be assigned to the client prefix; Default: )

allow-dual-stack-Creates a single simple queue entry for both IPv4 and IPv6 addresses, uses the MAC address and DUID for identification. Requires I queue (yes | no; Pv4 DHCP Server to have this option enabled as well to work properly. Default: yes)

comment (string; Short description of an item. Default: )

disabled (yes | Whether an item is disabled no; Default: no)

dhcp-option (stri Add additional DHCP options from option list. the ng; Default: )

dhcp-option-set ( Add an additional set of DHCP options. string; Default: )

life-time (time; The time period after which binding expires. Default: 3d)

duid (hex string; DUID value. Should be specified only in hexadecimal format. Default: )

iaid (integer [0.. Identity Association Identifier, part of the Client ID. 4294967295]; Default: )

prefix-pool (string Prefix pool that is being advertised to the DHCPv6 Client.; Default: )

rate-limit (integer Adds a dynamic simple queue to limit IP's bandwidth to a specified rate. Requires the lease to be static. Format is: rx-rate[/tx-rate] [rx- [/integer] [integer burst-rate[/tx-burst-rate] [rx-burst-threshold[/tx-burst-threshold] [rx-burst-time[/tx-burst-time]]]]. All rates should be numbers with [/integer] [integer optional 'k' (1,000s) or 'M' (1,000,000s). If tx-rate is not specified, rx-rate is as tx-rate too. Same goes for tx-burst-rate and tx-burst- [/integer] [integer threshold and tx-burst-time. If both rx-burst-threshold and tx-burst-threshold are not specified (but burst-rate is specified), rx-rate and [/integer]]]]; tx-rate is used as burst thresholds. If both rx-burst-time and tx-burst-time are not specified, 1s is used as default. Default: )

server (string | Name of the server. If set to all, then binding applies to all created DHCP-PD servers. all; Default: all)

Read-only properties

Property Description

dynamic (yes | Whether an item is dynamically created. no)

expires-after (ti The time period after which binding expires. me)

last-seen (time) Time period since the client was last seen.

status (waiting Three status values are possible: | offered | bound) waiting-Shown for static bindings if it is not used. For dynamic bindings this status is shown if it was used previously, the server will wait 10 minutes to allow an old client to get this binding, otherwise binding will be cleared and prefix will be offered to other clients. offered - if solicit message was received, and the server responded with advertise a message, but the request was not received. During this state client have 2 minutes to get this binding, otherwise, it is freed or changed status to waiting for static bindings. bound-currently bound.

reconfigure-Reconfiguration authentication key key (string)

reconfigure-Count of sent Reconfigure (forcerenew) messages last-sent (integ er)

reconfigure- status

For example, dynamically assigned /62 prefix

[admin@RB493G] /ipv6 dhcp-server binding> print detail Flags: X-disabled, D-dynamic 0 D address=2a02:610:7501:ff00::/62 duid="1605fcb400241d1781f7" iaid=0 server=local-dhcp life-time=3d status=bound expires-after=2d23h40m10s last-seen=19m50s 1 D address=2a02:610:7501:ff04::/62 duid="0019d1393535" iaid=2 server=local-dhcp life-time=3d status=bound expires-after=2d23h43m47s last-seen=16m13s

Menu specific commands

Property Description

make-static () Set dynamic binding as static.

send-reconfigure ( ) id Send Reconfigure (forcerenew) message

Rate limiting

It is possible to set the bandwidth to a specific IPv6 address by using DHCPv6 bindings. This can be done by setting a rate limit on the DHCPv6 binding itself, by doing this a dynamic simple queue rule will be added for the IPv6 address that corresponds to the DHCPv6 binding. By using the rate-limit parameter you can conveniently limit a user's bandwidth.the

For any queues to work properly, the traffic must not be FastTracked, make sure your Firewall does not FastTrack traffic that you want to limit.

First, make the DHCPv6 binding static, otherwise, it will not be possible to set a rate limit to a DHCPv6 binding:

[admin@MikroTik] > /ipv6 dhcp-server binding print Flags: X-disabled, D-dynamic # ADDRESS DUID SERVER STATUS 0 D fdb4:4de7:a3f8:418c::/66 0x6c3b6b7c413e DHCPv6_Server bound

[admin@MikroTik] > /ipv6 dhcp-server binding make-static 0

[admin@MikroTik] > /ipv6 dhcp-server binding print Flags: X-disabled, D-dynamic # ADDRESS DUID SERVER STATUS 0 fdb4:4de7:a3f8:418c::/66 0x6c3b6b7c413e DHCPv6_Server bound

Then you need can set a rate to a DHCPv6 binding that will create a new dynamic simple queue entry:

[admin@MikroTik] > /ipv6 dhcp-server binding set 0 rate-limit=10M/10 [admin@MikroTik] > /queue simple print Flags: X-disabled, I-invalid, D-dynamic 0 D name="dhcp<6c3b6b7c413e fdb4:4de7:a3f8:418c::/66>" target=fdb4:4de7:a3f8:418c::/66 parent=none packet- marks="" priority=8/8 queue=default -small/default-small limit-at=10M/10M max-limit=10M/10M burst-limit=0/0 burst-threshold=0/0 burst-time=0s/0s bucket-size=0.1/0.1

By default allow-dual-stack-queue is enabled, this will add a single dynamic simple queue entry for both DHCPv6 binding and DHCPv4 lease, without this option enabled separate dynamic simple queue entries will be added for IPv6 and IPv4.

If allow-dual-stack-queue is enabled, then a single dynamic simple queue entry will be created containing both IPv4 and IPv6 addresses:

[admin@MikroTik] > /queue simple print Flags: X-disabled, I-invalid, D-dynamic 0 D name="dhcp-ds<6C:3B:6B:7C:41:3E>" target=192.168.1.200/32,fdb4:4de7:a3f8:418c::/66 parent=none packet- marks="" priority=8/8 queue=default -small/default-small limit-at=10M/10M max-limit=10M/10M burst-limit=0/0 burst-threshold=0/0 burst-time=0s/0s bucket-size=0.1/0.1

### RADIUS Support

Since RouterOS v6.43 it is possible to use RADIUS to assign a rate-limit per DHCPv6 binding, to do so you need to pass the Mikrotik-Rate-Limit attribute from your RADIUS Server for your DHCPv6 binding. To achieve this you first need to set your DHCPv6 Server to use RADIUS for assigning bindings. Below is an example of how to set it up:

/radius add address=10.0.0.1 secret=VERYsecret123 service=dhcp /ipv6 dhcp-server set dhcp1 use-radius=yes

After that, you need to tell your RADIUS Server to pass the Mikrotik-Rate-Limit attribute. In case you are using FreeRADIUS with MySQL, then you need to add appropriate entries into radcheck and radreply tables for a MAC address, that is being used for your DHCPv6 Client. Below is an example for table entries:

INSERT INTO `radcheck` (`username`, `attribute`, `op`, `value`) VALUES ('000c4200d464', 'Auth-Type', ':=', 'Accept'), INSERT INTO `radreply` (`username`, `attribute`, `op`, `value`) VALUES ('000c4200d464', 'Delegated-IPv6-Prefix', '=', 'fdb4:4de7:a3f8:418c::/66'), ('000c4200d464', 'Mikrotik-Rate-Limit', '=', '10M');

By default allow-dual-stack-queue is enabled and will add a single dynamic queue entry if the MAC address from the IPv4 lease (or DUID, if the DHCPv4 Client supports Node-specific Client Identifiers from RFC4361), but DUID from DHCPv6 Client is not always based on the MAC address from the interface on which the DHCPv6 client is running on, DUID is generated on a per-device basis. For this reason, a single dynamic queue entry might not be created, separate dynamic queue entries might be created instead.

### Configuration Example

Enabling IPv6 Prefix delegation

Let's consider that we already have a running DHCP server.

To enable IPv6 prefix delegation, first, we need to create an address pool:

/ipv6 pool add name=myPool prefix=2001:db8:7501::/60 prefix-length=62

Notice that prefix-length is 62 bits, which means that clients will receive /62 prefixes from the /60 pool.

The next step is to enable DHCP-PD:

/ipv6 dhcp-server add name=myServer prefix-pool=myPool interface=local

To test our server we will set up wide-dhcpv6 on an ubuntu machine:

install wide-dhcpv6-client edit "/etc/wide-dhcpv6/dhcp6c.conf" as above

You can use also RouterOS as a DHCP-PD client.

interface eth2{ send ia-pd 0; };

id-assoc pd { prefix-interface eth3{ sla-id 1; sla-len 2; }; };

Run DHCP-PD client:

sudo dhcp6c -d -D -f eth2

Verify that prefix was added to the:

mrz@bumba:/media/aaa$ ip -6 addr .. 2: eth3: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qlen 1000 inet6 2001:db8:7501:1:200:ff:fe00:0/64 scope global valid_lft forever preferred_lft forever inet6 fe80::224:1dff:fe17:81f7/64 scope link valid_lft forever preferred_lft forever

You can make binding to specific client static so that it always receives the same prefix:

[admin@RB493G] /ipv6 dhcp-server binding> print Flags: X-disabled, D-dynamic # ADDRESS DU IAID SER.. STATUS 0 D 2001:db8:7501:1::/62 16 0 loc.. bound [admin@RB493G] /ipv6 dhcp-server binding> make-static 0

DHCP-PD also installs a route to assigned prefix into IPv6 routing table:

[admin@RB493G] /ipv6 route> print Flags: X-disabled, A-active, D-dynamic, C-connect, S-static, r-rip, o-ospf, b-bgp, U-unreachable # DST-ADDRESS GATEWAY DISTANCE ... 2 ADS 2001:db8:7501:1::/62 fe80::224:1dff:fe17:8... 1

Enabling IPv6 Address delegation

Address delegation on DHCPv6 server side works almost in the exact same way as when you configure prefix server. Only difference is that you must specify in configuration address-pool instead of prefix-pool and the pool used for this server must be defined to use /128 prefix-length. Of course, you can create server which only assigns static addresses and skip using the pool.

[admin@MikroTik] > ipv6/pool/print detail Flags: D-dynamic 0 name="myAddressPool" prefix=2001:db8:7501::/120 prefix-length=128 [admin@MikroTik] > /ipv6/dhcp-server/print detail Flags: D-dynamic; X-disabled, I-invalid 0 name="myDHCP" interface=ether2 prefix-pool=static-only address-pool=myAddressPool lease-time=3d rapid-commit=yes use-radius=no preference=255 dhcp-option="" route-distance=1 use-reconfigure=no address-lists="" duid="0x00030001b813f4840556"

This configuration is already enough to work with DHCPv6 clients such as, for example, RouterOS client.

[admin@MikroTik] > ipv6/dhcp-client/print detail Flags: D-dynamic; X-disabled, I-invalid 0 interface=ether2 status=bound duid="0x00030001b123f48407f0" dhcp-server-v6=fe80::ba69:f4af:fe14:558 request=address add-default-route=no use-peer-dns=yes allow-reconfigure=no dhcp-options="" pool-name="" pool-prefix-length=64 prefix-hint=::/0 prefix-address-lists="" dhcp-options="" address=2001:db8:7501::, 2d23h59m51s

However, usually end-devices as computers do not know if their network is managed by DHCP server or not. That is why DHCPv6 server configuration is combined with SLAAC functionality. You can even avoid using SLAAC in order to advertise prefix for local network device, all you need to do is advertise "managed-address-configuration" option to your network devices.

[admin@MikroTik] > ipv6/nd/print detail Flags: X-disabled, I-invalid; * - default 0 interface=ether2 ra-interval=3m20s-10m ra-delay=3s mtu=unspecified reachable-time=unspecified retransmit-interval=unspecified ra-lifetime=30m ra-preference=medium hop-limit=unspecified advertise-mac-address=yes advertise-dns=yes managed-address-configuration=yes other-configuration=no [admin@MikroTik] > ipv6/nd/prefix/print detail Flags: X-disabled, I-invalid; D-dynamic 0 prefix=::/64 6to4-interface=none interface=ether2 on-link=yes autonomous=yes valid-lifetime=4w2d preferred-lifetime=1w

Now, for example, your computer which will be connected to router ether2 interface will receive advertisement message from RouterOS ND configuration stating that this network is using "managed-address-configuration" which normally on end user devices will enable DHCPv6 client requesting IPv6 address.

Full configuration backup from the server with several comments is provided here.

#Address pool to be used for 'bridge', must have prefix-length 128 /ipv6 pool add name=myLocalLan prefix=2001:db8::/100 prefix-length=128 #DHCPv6 server with spcified 'address' pool /ipv6 dhcp-server add address-pool=myLocalLan interface=bridge name=myLocalServer prefix-pool="" #We must 'advertise' that this is managed network so LAN devices use DHCPv6 clients #RFC 4861, RFC 4862, RFC 8415 'M-Managed address configuration' /ipv6 nd add interface=bridge managed-address-configuration=yes #We must enable advertising on our 'bridge' interface #We can even add interface without specified prefix, because we here need only #to advertise 'option' that tells this is managed network /ipv6 nd prefix add interface=bridge

Server configuration might vary based on operating systems used by clients. For example, macOS will get an address on initialisation with such configuration but might not renew lease after sleep, if prefix is set to "none", since macOS does not use DHCPv6 client without SLAAC address. Other clients might need also "autonomous" option to be set to "no" in order to trigger DHCPv6 client usage. This is just a configuration example

- settings might need adjustments depending on client devices.
