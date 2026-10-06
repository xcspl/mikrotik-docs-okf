---
type: Reference
title: "Summary"
description: "The DHCP (Dynamic Host Configuration Protocol) is used for the easy distribution of IP addresses in a network. The MikroTik RouterOS implementation includes both server and client parts and is compliant with RFC 2131."
timestamp: '2026-10-06'
status: active
tags: [routeros, mikrotik, networking]
resource: ~/Downloads/ROS-260526-1445-796.pdf
sources:
  - resource: https://manual.mikrotik.com/docs/introduction/
---

# Summary

The DHCP (Dynamic Host Configuration Protocol) is used for the easy distribution of IP addresses in a network. The MikroTik RouterOS implementation includes both server and client parts and is compliant with RFC 2131.

The router supports an individual server for each Ethernet-like interface. The MikroTik RouterOS DHCP server supports the basic functions of giving each requesting client an IP address/netmask lease, default gateway, domain name, DNS-server(s) and WINS-server(s) (for Windows clients) information (set up in the DHCP networks submenu)

In order for the DHCP server to work, IP pools must also be configured (do not include the DHCP server's own IP address into the pool range) and the DHCP networks.

It is also possible to hand out leases for DHCP clients using the RADIUS server; the supported parameters for a RADIUS server are as follows:

Access-Request:

NAS-Identifier-router identity NAS-IP-Address-IP address of the router itself NAS-Port-the ID of the interface where the DHCP server is configured. This value is the same as the IF-MIB::ifIndex NAS-Port-Id-the name of the interface where the DHCP server is configured NAS-Port-Type-Ethernet Calling-Station-Id-client identifier (active-client-id) Framed-IP-Address-IP address of the client (active-address) Called-Station-Id-the name of DHCP server User-Name-MAC address of the client (active-mac-address) Password - " "

Access-Accept:

Framed-IP-Address-IP address that will be assigned to a client Framed-Pool-IP pool from which to assign an IP address to a client Rate-Limit-Datarate limitation for DHCP clients. Format is: rx-rate[/tx-rate] [rx-burst-rate[/tx-burst-rate] [rx-burst-threshold[/tx-burst-threshold] [rx- burst-time[/tx-burst-time][priority] [rx-rate-min[/tx-rate-min]]]]. All rates should be numbers with optional 'k' (1,000s) or 'M' (1,000,000s). If tx-rate is not specified, rx-rate is as tx-rate too. Same goes for tx-burst-rate and tx-burst-threshold and tx-burst-time. If both rx-burst-threshold and tx-burst- threshold are not specified (but burst-rate is specified), rx-rate and tx-rate are used as burst thresholds. If both rx-burst-time and tx-burst-time are not specified, 1s is used as default. Priority takes values 1..8, where 1 implies the highest priority, but 8 - the lowest. If rx-rate-min and tx-rate-min are not specified rx-rate and tx-rate values are used. The rx-rate-min and tx-rate-min values can not exceed rx-rate and tx-rate values. Ascend-Data-Rate-TX/RX data rate limitation if multiple attributes are provided, first limits tx data rate, second-RX data rate. If used together with Ascend-Xmit-Rate, specifies RX rate. 0 if unlimited Ascend-Xmit-Rate-tx data rate limitation. It may be used to specify the TX limit only instead of sending two sequential Ascend-Data-Rate attributes (in that case Ascend-Data-Rate will specify the receive rate). 0 if unlimited Session-Timeout-max lease time (lease-time)

DHCP server requires a real interface to receive raw ethernet packets. If the interface is a Bridge interface, then the Bridge must have a real interface attached as a port to that bridge which will receive the raw ethernet packets. It cannot function correctly on a dummy (empty bridge) interface.

### DHCP Server Properties

Property Description

add-arp (yes | no; Default: no) Whether to add dynamic ARP entry. If set to no either ARP mode should be enabled on that interface or st atic ARP entries should be administratively defined in /ip arp submenu.

address-pool (string | static-only; IP pool, from which to take IP addresses for the clients. If set to static-only, then only the clients that have a static Default: static-only) lease (added in lease submenu) will be allowed. the

allow-dual-stack-queue (yes | no; Default: yes)

always-broadcast (yes | no; Default: no)

authoritative (after-10sec-delay | after-2sec-delay | yes | no; Default: yes)

bootp-lease-time (forever | lease- time | time; Default: forever)

bootp-support (none | static | dynamic; Default: static)

client-mac-limit (integer | unlimited; Default: unlimited)

conflict-detection (yes | no; Default: yes)

delay-threshold (time | none; Default: none)

dhcp-option-set (name | none; Default: none)

dynamic-lease-identifiers (list of client-id, client-mac. opt-82; Default: client-id,client-mac)

insert-queue-before (bottom | first | name; Default: first)

interface (string; Default: )

Creates a single simple queue entry for both IPv4 and IPv6 addresses, and uses the MAC address and DUID for identification. Requires IPv6 DHCP Server to have this option enabled as well to work properly.

Changes whether to force broadcast DHCP replies:

no-replies are sent based on the client's broadcast flag. If the server sends three consecutive offers, the third and forth offer will be sent as a broadcast; yes-replies are always broadcasted even when the client has not specified the broadcast flag.

Option changes the way how a server responds to DHCP requests:

yes-replies to clients' requests for an address that is not available from this server, DHCP server will send a negative acknowledgment (DHCPNAK); no-DHCP server ignores clients' requests for addresses that are not available from this server;

after-10sec-delay-requests with "secs < 10" will be processed as in "no" setting case and requests with "secs >= 10" will be processed as in "yes" case;

after-2sec-delay-requests with "secs < 2" will be processed as in "no" setting case and requests with "secs >= 2" will be processed as in "yes" case;

If all requests with "secs < x" should be ignored, then delay-threshold=x setting should be used.

Accepts two predefined options or time value:

forever-lease never expires lease-time-use time from lease-time parameter

Support for BOOTP clients:

none-do not respond to BOOTP requests static-offer only static leases to BOOTP clients dynamic-offer static and dynamic leases for BOOTP clients

Specifies whether to limit a specific number of clients per single MAC address or leave unlimited. Note that this setting should not be used in relay setups.

Allows disabling/enabling conflict detection. If the option is enabled, then whenever the server tries to assign a lease it will send ICMP and ARP messages to detect whether such an address in the network already exists. If any of the above get a reply address is considered already used.

If the sec's field in the DHCP packet is smaller than the delay threshold, then this packet is ignored. If set to none-there is no threshold (all DHCP packets are processed)

Use a custom set of DHCP options defined in the option sets menu.

Specify which parameters to use and store when generating a dynamic DHCP lease.

Specify where to place dynamic simple queue entries for static DHCP leases with rate-limit parameter set. a

The interface on which the DHCP server will be running.

lease-script (string; Default: "") A script that will be executed after a lease is assigned or de-assigned. Internal "global" variables that can be used in the script:

leaseBound-set to "1" if bound, otherwise set to "0" leaseServerName-DHCP server name leaseActMAC-active mac address leaseActIP-active IP address lease-agent-circuit-id-lease agent circuit ID lease-agent-remote-id-lease agent remote ID lease-hostname-client hostname lease-options-an array of received options

lease-time (time; Default: 30m) The time that a client may use the assigned address. The client will try to renew this address after half of this time and will request a new address after the time limit expires.

name (string; Default: ) Reference name

parent-queue (string | none; A dynamically created queue for this lease will be configured as a child queue of the specified parent queue. Default: none)

relay (IP; Default: 0.0.0.0) The IP address of the relay this DHCP server should process requests from:

0.0.0.0 - the DHCP server will be used only for direct requests from clients (no DHCP relay allowed)
255.255.255.255 - the DHCP server should be used for any incoming request from a DHCP relay except for those, which are processed by another DHCP server that exists in the /ip dhcp-server submenu.
server-address (IP; Default: 0.0.0.0 The IP address of the server to use in the next step of the client's bootstrap process (For example, to assign a ) specific server address in case several addresses are assigned to the interface)

support-broadband-tr101 (yes | no Enables or disables the inclusion of additional Option 82 suboptions (e.g. 0x81 actual upstream, 0x82 actual; Default: no) downstream) in RADIUS Access-Request and Accounting-Request messages as described in RFC 4679 and Broadband Forum TR-101.

When enabled, the DHCP server includes specific suboptions under DHCP Option 82 (Relay Agent Information) that are used by RADIUS servers to identify subscriber line parameters in broadband access networks, especially those based on DSL infrastructure.

This property only has an effect when use-radius is set to yes or accounting.

use-framed-as-classless (yes | no; Forward RADIUS Framed-Route as a DHCP Classless-Static-Route to DHCP-client. Whenever both Framed- Default: yes) Route and Classless-Static-Route are received Classless-Static-Route is preferred.

use-radius (yes | no | accounting; Whether to use RADIUS server: Default: no) no-do not use RADIUS; yes-use RADIUS for accounting and lease; accounting-use RADIUS for accounting only.

use-reconfigure (yes | no; Default: Allow the server to send Reconfigure (forcerenew) messages to clients, prompting them to renew configuration no) without waiting for their lease to expire.

Leases

Sub-menu: /ip dhcp-server lease

DHCP server lease submenu is used to monitor and manage server leases. The issued leases are shown here as dynamic entries. You can also add static leases to issue a specific IP address to a particular client (identified by MAC address).

Generally, the DHCP lease is allocated as follows:

an unused lease is in the "waiting" state if a client asks for an IP address, the server chooses one if the client receives a statically assigned address, the lease becomes offered, and then bound with the respective lease time if the client receives a dynamic address (taken from an IP address pool), the router sends a ping packet and waits for an answer for 0.5 seconds. During this time, the lease is marked testing

in the case where the address does not respond, the lease becomes offered and then bound with the respective lease time in other cases, the lease becomes busy for the lease time (there is a command to retest all busy addresses), and the client's request remains unanswered (the client will try again shortly)

A client may free the leased address. The dynamic lease is removed, and the allocated address is returned to the address pool. But the static lease becomes busy until the client reacquires the address.

IP addresses assigned statically are not probed!

Property Description

address (IP; Default: 0.0.0.0) Specify IP address (or ip pool) for static lease. If set to 0.0.0.0 - a pool from the DHCP server will be used

address-list (string; Default: none) Address list to which address will be added if the lease is bound.

agent-circuit-id (hex string; Defaul If specified, value must match the Option 82 Agent Circuit ID suboption of the request. t none)

agent-remote-id (hex string; Defa If specified, value must match the Option 82 Agent Remote ID suboption of the request. ult none)

allow-dual-stack-queue (yes | no; Creates a single simple queue entry for both IPv4 and IPv6 addresses, and uses the MAC address and DUID Default: yes) for identification. Requires IPv6 DHCP Server to have this option enabled as well to work properly.

always-broadcast (yes | no; Changes whether to force broadcast DHCP replies: Default: no) no-replies are sent based on the client's broadcast flag. If the server sends three consecutive offers, the third and forth offer will be sent as a broadcast; yes-replies are always broadcasted even when the client has not specified the broadcast flag.

block-access (yes | no; Default: no Block access for this client )

client-id (string; Default: none) If specified, must match the DHCP 'client identifier' option of the request

dhcp-option (string; Default: none) Add additional DHCP options from option list.

dhcp-option-set (string; Default: n Add an additional set of DHCP options. one)

insert-queue-before (bottom | Specify where to place dynamic simple queue entries for static DHCP leases with rate-limit parameter set. first | name; Default: first)

lease-time (time; Default: 0s) Time that the client may use the address. If set to 0s lease will never expire.

mac-address (MAC; Default: 00: If specified, must match the MAC address of the client 00:00:00:00:00)

parent-queue (string | none; A dynamically created queue for this lease will be configured as a child queue of the specified parent queue. Default: none)

queue-type (default, ethernet-Queue type that can be assigned to the specific lease default, multi-queue-ethernet- default, pcq-download-default, synchronous-default, default- small, hotspot-default, only- hardware-queue, pcq-upload- default, wireless-default)

rate-limit (integer[/integer] [integer Adds a dynamic simple queue to limit IP's bandwidth to a specified rate. Requires the lease to be static. Format [/integer] [integer[/integer] [integer is: rx-rate[/tx-rate] [rx-burst-rate[/tx-burst-rate] [rx-burst-threshold[/tx-burst-threshold] [rx-burst-time[/tx-burst- [/integer]]]];; Default: ) time]]]]. All rates should be numbers with optional 'k' (1,000s) or 'M' (1,000,000s). If tx-rate is not specified, rx- rate is as tx-rate too. Same goes for tx-burst-rate and tx-burst-threshold and tx-burst-time. If both rx-burst- threshold and tx-burst-threshold are not specified (but burst-rate is specified), rx-rate and tx-rate is used as burst thresholds. If both rx-burst-time and tx-burst-time are not specified, 1s is used as default.

routes ([dst-address/mask] Routes that appear on the server when the client is connected. It is possible to specify multiple routes [gateway] [distance]; Default: none separated by commas. This setting will be ignored for OpenVPN. )

server (string) Server name which serves this client

use-src-mac (yes | no; Default: no) When this option is set server uses the source MAC address instead of the received CHADDR to assign the address.

status (waiting | testing | declined Shows the status of DHCP lease: | offered | bound | authorizing | conflict) waiting-waiting for static DHCP lease to get bound testing-checking for ARP conflicts declined-DHCP client replied with decline packet offered-server offered address to DHCP client, but did not yet receive DHCP request back bound-DHCP client accepted DHCP lease authorizing-communicating with RADIUS conflict-ARP conflict detected

Menu specific commands

check-status ( ) id Check the status of a given busy (status is conflict or declined) dynamic lease, and free it in case of no response

make-static ( ) id Convert a dynamic lease to a static one

send-reconfigure ( ) id Send Reconfigure (forcerenew) message

Store Configuration

Sub-menu: /ip dhcp-server config

Store Leases On Disk: The configuration of how often the DHCP leases will be stored on disk. If they would be saved on a disk on every lease change, a lot of disk writes would happen which is very bad for Compact Flash (especially, if lease times are very short). To minimize writes on disk, all changes are saved on disk every store-leases-disk seconds. Additionally, leases are always stored on disk on graceful shutdown and reboot.

Manual changes to leases-addition/removal of a static lease, removal of a dynamic lease will cause changes to be pushed for this lease to storage.

Accounting: The accounting parameter in the DHCP server configuration enables or disables accounting for DHCP leases. When accounting is enabled, the DHCP server logs information about IP address assignments and lease renewals. This information can be useful for tracking and monitoring network usage, analyzing traffic patterns, or generating reports on IP address allocations.

Interim-update: The interim-update parameter determines whether the DHCP server sends periodic updates to the accounting server during a lease. These updates provide information about the lease duration, usage, and other relevant details. Enabling interim updates allows for more accurate tracking of lease activity.

Radius-password: The radius-password parameter is used to set the password for the RADIUS (Remote Authentication Dial-In User Service) server. RADIUS is a networking protocol commonly used for providing centralized authentication, authorization, and accounting for network access. When configuring the DHCP server to communicate with a RADIUS server for authentication or accounting purposes, you need to specify the correct password to establish a secure connection. This parameter ensures that the DHCP server can authenticate with the RADIUS server using the specified password.

Rate limiting

It is possible to set the bandwidth to a specific IPv4 address by using DHCPv4 leases. This can be done by setting a rate limit on the DHCPv4 lease itself, by doing this a dynamic simple queue rule will be added for the IPv4 address that corresponds to the DHCPv4 lease. By using the rate-limit parameter you can conveniently limit a user's bandwidth.

For any queues to work properly, the traffic must not be FastTracked, make sure your Firewall does not FastTrack traffic that you want to limit.

First, make the DHCPv4 lease static, otherwise, it will not be possible to set a rate limit to a DHCPv4 lease:

[admin@MikroTik] > /ip dhcp-server lease print Flags: X-disabled, R-radius, D-dynamic, B-blocked # ADDRESS MAC-ADDRESS HOST-NAME SERVER RATE- LIMIT STATUS 0 D 192.168.88.254 6C:3B:6B:7C:41:3E MikroTik DHCPv4_Server bound

[admin@MikroTik] > /ip dhcp-server lease make-static 0

[admin@MikroTik] > /ip dhcp-server lease print Flags: X-disabled, R-radius, D-dynamic, B-blocked # ADDRESS MAC-ADDRESS HOST-NAME SERVER RATE- LIMIT STATUS 0 192.168.88.254 6C:3B:6B:7C:41:3E MikroTik DHCPv4_Server bound

Then you can set a rate to a DHCPv4 lease that will create a new dynamic simple queue entry:

[admin@MikroTik] > /ip dhcp-server lease set 0 rate-limit=10M/10M

[admin@MikroTik] > /queue simple print Flags: X-disabled, I-invalid, D-dynamic 0 D name="dhcp-ds<6C:3B:6B:7C:41:3E>" target=192.168.88.254/32 parent=none packet-marks="" priority=8/8 queue=default-small/default-small limit-at=10M/10M max-limit=10M/10M burst-limit=0/0 burst-threshold=0/0 burst- time=0s/0s bucket-size=0.1/0.1

By default allow-dual-stack-queue is enabled, this will add a single dynamic simple queue entry for both DHCPv6 binding and DHCPv4 lease, without this option enabled separate dynamic simple queue entries will be added for IPv6 and IPv4.

If allow-dual-stack-queue is enabled, then a single dynamic simple queue entry will be created containing both IPv4 and IPv6 addresses:

[admin@MikroTik] > /queue simple print Flags: X-disabled, I-invalid, D-dynamic 0 D name="dhcp-ds<6C:3B:6B:7C:41:3E>" target=192.168.88.254/32,fdb4:4de7:a3f8:418c::/66 parent=none packet- marks="" priority=8/8 queue=default-small/default-small limit-at=10M/10M max-limit=10M/10M burst-limit=0/0 burst-threshold=0/0 burst-time=0s/0s bucket-size=0.1/0.1

Network

Sub-menu: /ip dhcp-server network

Properties

Property Description

address (IP the network DHCP server(s) will lease addresses from /netmask; Default: )

boot-file-name ( Boot filename string; Default: )

caps-manager ( A comma-separated list of IP addresses for one or more CAPsMAN system managers. DHCP Option 138 (capwap) will be used. string; Default: )

dhcp-option (stri Add additional DHCP options from option list. the ng; Default: )

dhcp-option-set ( Add an additional set of DHCP options. string; Default: )

dns-none (yes | If set, then DHCP Server will not pass DNS servers configured on the router to the DHCP clients. no; Default: no)

dns-server (string DNS servers that will be passed to DHCP clients. Two comma-separated DNS servers can be specified to be used by the DHCP; Default: ) client as primary and secondary DNS servers

By default, if there are no DNS servers configured, then the router dynamic DNS Servers from IP>DNS will be passed to DHCP clients, if there are no dynamic DNS server configured, the router static DNS servers from IP>DNS will be passed to DHCP clients.

domain (string; The DHCP client will use this as the 'DNS domain' setting for the network adapter. Default: )

gateway (IP; The default gateway to be used by DHCP Client. Default: 0.0.0.0)

netmask (intege The actual network mask is to be used by the DHCP client. If set to '0' - netmask from network address will be used. r: 0..32; Default:

0) next-server (IP; The IP address of the next server to use in bootstrap. Default: ) ntp-none (yes | If set, then DHCP Server will not pass NTP servers configured on the router to the DHCP clients. no; Default: no) ntp-server (IP; the DHCP client will use these as the default NTP servers. Two comma-separated NTP servers can be specified to be used by Default: ) the DHCP client as primary and secondary NTP servers wins-server (IP; The Windows DHCP client will use these as the default WINS servers. Two comma-separated WINS servers can be specified to Default: ) be used by the DHCP client as primary and secondary WINS servers
### RADIUS Support

Since RouterOS v6.43 it is possible to use RADIUS to assign a rate limit per lease, to do so you need to pass the Mikrotik-Rate-Limit attribute from your RADIUS Server for your lease. To achieve this you first need to set your DHCPv4 Server to use RADIUS for assigning leases. Below is an example of how to set it up:

/radius add address=10.0.0.1 secret=VERYsecret123 service=dhcp /ip dhcp-server set dhcp1 use-radius=yes

Mikrotik-Rate-LimitAfter that, you need to tell your RADIUS Server to pass the attribute. In case you are using FreeRADIUS with MySQL, then you need to add appropriate entries into radcheck and radreply tables for a MAC address, that is being used for your DHCPv4 Client. Below is an example for table entries:

INSERT INTO `radcheck` (`username`, `attribute`, `op`, `value`) VALUES ('00:0C:42:00:D4:64', 'Auth-Type', ':=', 'Accept'),

INSERT INTO `radreply` (`username`, `attribute`, `op`, `value`) VALUES ('00:0C:42:00:D4:64', 'Framed-IP-Address', '=', '192.168.88.254'), ('00:0C:42:00:D4:64', 'Mikrotik-Rate-Limit', '=', '10M'),

Alerts

To find any rogue DHCP servers as soon as they appear in your network, the DHCP Alert tool can be used. It will monitor the interface for all DHCP replies and check if this reply comes from a valid DHCP server. If a reply from an unknown DHCP server is detected, an alert gets triggered:

[admin@MikroTik] ip dhcp-server alert>/log print 00:34:23 dhcp,critical,error,warning,info,debug dhcp alert on Public: discovered unknown dhcp server, mac 00:02:29:60:36:E7, ip 10.5.8.236 [admin@MikroTik] ip dhcp-server alert>

When the system alerts about a rogue DHCP server, it can execute a custom script.

As DHCP replies can be unicast, the rogue DHCP detector may not receive any offer to other DHCP clients at all. To deal with this, the rogue DHCP detector acts as a DHCP client as well-it sends out DHCP discover requests once a minute.

The DHCP alert is not recommended on devices that are configured as DHCP clients. Since the alert itself generates DHCP discovery packets, it can affect the operation of the DHCP client itself. Use this feature only on devices that are DHCP servers or using a static IP address.

Sub-menu: /ip dhcp-server alert

|Properties|||
|---|---|---|
|Property||Description|
|alert-timeout (none | time;||Time after which the alert will be forgotten. If after that time the same server is detected, a new alert will be generated.|
|Default: 1h)||If set to none timeout will never expire.|
|interface (string; Default: )||Interface, on which to run rogue DHCP server finder.|
|on-alert (string; Default: )||Script to run, when an unknown DHCP server is detected.|
|valid-server (string; Default:||List of MAC addresses of valid DHCP servers.|
|)|||
|Read-only properties|||
|Property||Description|
|unknown-server (string)||List of MAC addresses of detected unknown DHCP servers. The server is removed from this list after alert-timeout|
|Menu specific commands|||
|Property|Description||
|reset-alert ( )|id Clear all alerts on an interface||

### DHCP Options

Sub-menu: /ip dhcp-server option

With the help of the DHCP Option list, it is possible to define additional custom options for DHCP Server to advertise. Option precedence is as follows:

radius, lease, server, network.

This is the order in which the client option request will be filled in.

According to the DHCP protocol, a parameter is returned to the DHCP client only if it requests this parameter, specifying the respective code in the DHCP request Parameter-List (code 55) attribute. If the code is not included in the Parameter-List attribute, the DHCP server will not send it to the DHCP client, but since RouterOS v7.1rc5 it is possible to force the DHCP option from the server-side even if the DHCP-client does not request such parameter:

ip/dhcp-server/option/set force=yes

Properties

Property Description

code (integer:1..254; dhcp option code. All codes are available at http://www.iana.org/assignments/bootp-dhcp-parameters Default: )

name (string; Default: ) Descriptive name of the option

value (string; Default: ) Parameter's value. Available data types for options are:

'test' -> ASCII to Hex 0x74657374 '10.10.10.10' -> Unicode IP to Hex 0x0a0a0a0a s'10.10.10.10' -> ASCII to hex 0x31302e31302e31302e3130 s'160' -> ASCII to hex 0x313630 '10' -> Decimal to Hex 0x0a 0x0a0a -> No conversion $(VARIABLE) -> hardcoded values

RouterOS has predefined variables that can be used:

HOSTNAME-client hostname RADIUS_MT_STR1 - from radius MT attr nr. 24 RADIUS_MT_STR2 - from radius MT attr nr. 25 REMOTE_ID-agent remote-id NETWORK_GATEWAY-the first gateway from '/ip dhcp-server network', note that this option won't work if used from lease

Now it is also possible to combine data types into one, for example: "0x01'vards'$(HOSTNAME)"

For example if HOSTNAME is 'kvm', then raw value will be 0x0176617264736b766d.

raw-value (HEX string ) Read-only field which shows raw DHCP option value (the format actually sent out)

DHCP Option Sets

Sub-menu: /ip dhcp-server option sets

This menu allows combining multiple options in option sets, which later can be used to override the default DHCP server option set.

Example

Classless Route

A classless route adds a specified route in the clients routing table. In our example, it will add

dst-address=160.0.0.0/24 gateway=10.1.101.1 dst-address=0.0.0.0/0 gateway=10.1.101.1

According to RFC 3442: The first part is the netmask ("18" = netmask /24). Second part is significant part of destination network ("A00000" = 160.0.0). Third part is IP address of gateway ("0A016501" = 10.1.101.1). Then There are parts of the default route, destination netmask (0x00 = 0.0.0.0/0) followed by default route (0x0A016501 = 10.1.101.1)

/ip dhcp-server option add code=121 name=classless value=0x18A000000A016501000A016501 /ip dhcp-server network set 0 dhcp-option=classless

Result:

[admin@MikroTik] /ip route> print Flags: X-disabled, A-active, D-dynamic, C-connect, S-static, r-rip, b-bgp, o-ospf, m-mme, B-blackhole, U-unreachable, P-prohibit # DST-ADDRESS PREF-SRC GATEWAY DISTANCE 0 ADS 0.0.0.0/0 10.1.101.1 0 1 ADS 160.0.0.0/24 10.1.101.1 0

A much more robust way would be to use built-in variables, the previous example can be rewritten as:

/ip dhcp-server option add name=classless code=121 value="0x18A00000\$(NETWORK_GATEWAY)0x00\$(NETWORK_GATEWAY)"

Auto proxy config

/ip dhcp-server option add code=252 name=auto-proxy-config value="'https://autoconfig.something.lv/wpad.dat'"

### Option matcher

The Option matcher allows to identify DHCP clients by any of DHCP options and assign IP address from specific IP pool.

It is possible to perform exact (provided value should match exactly ) or  substring matching (will look for value match anywhere in the option string — it can match values at the start, middle, or end).

Substring matching is useful in cases where value can change depending on the end device, for example, if the class-identifier sent by the device contains not only vendor information, but also exact MAC or other additional information.

It's possible to define two substring matches for the same option, for example, one that matches "ABC" and another one that matches "ABCDE", if there is a DHCP option with the value of "ABCDEF", both entries would match it, but the matcher that will get applied will be selected randomly.

Clients with a static lease will continue to receive their static address, even when matched by the option matcher.

|Properties|||
|---|---|---|
|Property|Description||
|address-pool (string | static-only;|IP pool, from which to take IP addresses for the clients. If set to static-only, then only clients that have a static||
|Default: static-only)|lease (added in|lease submenu) will be allowed.the|
|code (integer:1..254; Default: )|DHCP option code. All codes are available at http://www.iana.org/assignments/bootp-dhcp-parameters||
|comment (string; Default: )|Short description of option matcher.||
|disabled (yes | no; Default: no)|Whether an item is disabled||
|matching-type (exact | substring;|Matching method:||
|Default: )|exact - option should match exactly to value; substring  value|-can match anywhere in the option string — at the start, middle, or end.|

|ne)|name (string; Default:) option-set (name | none; Default: no server (string all | value (string; Default:) Option matcher examples|; Default:)||Descriptive name for option matcher. A custom set of DHCP options defined in the Option Sets menu. Server name which serves option matcher. A value that will be searched for in option. Available data types for value are: string; HEX. Match dhcp1 server clients by exact Vendor class identifier (DHCP option 60) and assign address from the pool1:|
|---|---|---|---|---|
||/ip dhcp-server matcher /ip dhcp-server matcher /ip dhcp-server matcher|||add address-pool=pool1 code=60 matching-type=exact name=test1 server=dhcp1 value=android-dhcp-11 Match clients on all DHCP servers by exact Client Id (DHCP option 61) configured as hex value and assign address from the pool2: add address-pool=pool2 code=61 matching-type=exact name=test2 server=all value=0x016c3b6bed8364 Match dhcp2 server clients partially by Hostname (DHCP option 12) and assign address from the pool3: add address-pool=pool3 code=12 matching-type=substring name=test3 server=dhcp2 value=MikroTik|
|Setup|Configuration Examples Then you use setup a command which will automatically ask necessary parameters:|To simply configure DHCP server you can use a setup command. First, you configure an IP address on the interface:||[admin@MikroTik] > /ip address add address=192.168.88.1/24 interface=ether3 disabled=no|

[admin@MikroTik] > /ip dhcp-server setup Select interface to run DHCP server on

dhcp server interface: ether3 Select network for DHCP addresses

dhcp address space: 192.168.88.0/24 Select gateway for given network

gateway for dhcp network: 192.168.88.1 Select pool of ip addresses given out by DHCP server

addresses to give out: 192.168.88.2-192.168.88.254 Select DNS servers

dns servers: 10.155.126.1,10.155.0.1, Select lease time

lease time: 10m

That is all. You have configured an active DHCP server.

Manual configuration

To configure the DHCP server manually to respond to local requests you have to configure the following:

An IP pool for addresses to be given out, make sure that your gateway/DHCP server address is not part of the pool.

/ip pool add name=dhcp_pool0 ranges=192.168.88.2-192.168.88.254

A network indicating subnets that DHCP-server will lease addresses from, among other information, like a gateway, DNS-server, NTP-server, DHCP options, etc.

/ip dhcp-server network add address=192.168.88.0/24 dns-server=192.168.88.1 gateway=192.168.88.1

In our case, the device itself is serving as the gateway, so we'll add the address to the bridge interface:

/ip address add address=192.168.88.1/24 interface=bridge1 network=192.168.88.0

And finally, add DHCP Server, here we will add the previously created address pool, and specify on which interface the DHCP server should work on

/ip dhcp-server add address-pool=dhcp_pool0 disabled=no interface=bridge1 name=dhcp1
