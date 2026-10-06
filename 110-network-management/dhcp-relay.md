---
type: Reference
title: "DHCP Relay"
description: "The purpose of the DHCP relay is to act as a proxy between DHCP clients and the DHCP server. It is useful in networks where the DHCP server is not on the same broadcast domain as the DHCP client."
timestamp: '2026-05-26'
status: active
tags: [routeros, mikrotik, networking]
resource: ~/Downloads/ROS-260526-1445-796.pdf
sources:
  - resource: https://manual.mikrotik.com/docs/introduction/
---

# DHCP Relay

Summary

Sub-menu: /ip dhcp-relay

The purpose of the DHCP relay is to act as a proxy between DHCP clients and the DHCP server. It is useful in networks where the DHCP server is not on the same broadcast domain as the DHCP client.

DHCP relay does not choose the particular DHCP server in the DHCP-server list, it just sends the incoming request to all the listed servers.

Properties

Property Description

add-relay-info (yes | Adds DHCP relay agent information if enabled according to RFC 3046. Agent Circuit ID Sub-option contains mac address of no; Default: no) an interface, Agent Remote ID Sub-option contains MAC address of the client from which request was received.

delay-threshold (time | If secs field in DHCP packet is smaller than delay-threshold, then this packet is ignored none; Default: none)

dhcp-server (IPv4 addr List of DHCP servers' IP addresses which should the DHCP requests be forwarded to ess [IPv4]; Default: )

interface (interface; Interface name the DHCP relay will be working on. Default: )

local-address (IP; The unique IP address of this DHCP relay needed for DHCP server to distinguish relays. If set to 0.0.0.0 - the IP address will Default: 0.0.0.0) be chosen automatically from addresses that are assigned to an interface a relay is running

relay-info-remote-id (st specified string will be used to construct Option 82 instead of client's MAC address. Option 82 consist of: interface from which ring; Default: ) packets was received + client mac address or relay-info-remote-id

name (string; Default: ) Descriptive name for the relay

local-address-as-src-ip Use local address as source address for Discover/Request packets sent to the DHCP server (yes | no; Default: no)

disabled (yes | no; Whether relay is disabled or not. By default, it is not disabled Default: no)

dhcp-server-vrf (vrf; Specifies the VRF on which the DHCP relay should operate. Default: main)

### Configuration Example

Let us consider that you have several IP networks 'behind' other routers, but you want to keep all DHCP servers on a single router. To do this, you need a DHCP relay on your network which will relay DHCP requests from clients to the DHCP server.

This example will show you how to configure a DHCP server and a DHCP relay that serves 2 IP networks - 192.168.1.0/24 and 192.168.2.0/24 that are behind a router DHCP-Relay.

IP Address Configuration

IP addresses of DHCP-Server:

[admin@DHCP-Server] ip address> print Flags: X-disabled, I-invalid, D-dynamic # ADDRESS NETWORK BROADCAST INTERFACE 0 192.168.0.1/24 192.168.0.0 192.168.0.255 To-DHCP-Relay 1 10.1.0.2/24 10.1.0.0 10.1.0.255 Public [admin@DHCP-Server] ip address>

IP addresses of DHCP-Relay:

[admin@DHCP-Relay] ip address> print Flags: X-disabled, I-invalid, D-dynamic # ADDRESS NETWORK BROADCAST INTERFACE 0 192.168.0.2/24 192.168.0.0 192.168.0.255 To-DHCP-Server 1 192.168.1.1/24 192.168.1.0 192.168.1.255 Local1 2 192.168.2.1/24 192.168.2.0 192.168.2.255 Local2 [admin@DHCP-Relay] ip address>

DHCP Server Setup

To setup 2 DHCP Servers on the DHCP-Server router add 2 pools. For networks 192.168.1.0/24 and 192.168.2.0:

/ip pool add name=Local1-Pool ranges=192.168.1.11-192.168.1.100 /ip pool add name=Local2-Pool ranges=192.168.2.11-192.168.2.100 [admin@DHCP-Server] ip pool> print # NAME RANGES 0 Local1-Pool 192.168.1.11-192.168.1.100 1 Local2-Pool 192.168.2.11-192.168.2.100 [admin@DHCP-Server] ip pool>

Create DHCP Servers:

/ip dhcp-server add interface=To-DHCP-Relay relay=192.168.1.1 \ address-pool=Local1-Pool name=DHCP-1 disabled=no /ip dhcp-server add interface=To-DHCP-Relay relay=192.168.2.1 \ address-pool=Local2-Pool name=DHCP-2 disabled=no [admin@DHCP-Server] ip dhcp-server> print Flags: X-disabled, I-invalid # NAME INTERFACE RELAY ADDRESS-POOL LEASE-TIME ADD-ARP 0 DHCP-1 To-DHCP-Relay 192.168.1.1 Local1-Pool 3d00:00:00 1 DHCP-2 To-DHCP-Relay 192.168.2.1 Local2-Pool 3d00:00:00 [admin@DHCP-Server] ip dhcp-server>

Configure respective networks:

/ip dhcp-server network add address=192.168.1.0/24 gateway=192.168.1.1 \ dns-server=159.148.60.20 /ip dhcp-server network add address=192.168.2.0/24 gateway=192.168.2.1 \ dns-server 159.148.60.20 [admin@DHCP-Server] ip dhcp-server network> print # ADDRESS GATEWAY DNS-SERVER WINS-SERVER DOMAIN 0 192.168.1.0/24 192.168.1.1 159.148.60.20 1 192.168.2.0/24 192.168.2.1 159.148.60.20 [admin@DHCP-Server] ip dhcp-server network>

DHCP Relay Config

Configuration of DHCP-Server is done. Now let's configure DHCP-Relay:

/ip dhcp-relay add name=Local1-Relay interface=Local1 \ dhcp-server=192.168.0.1 local-address=192.168.1.1 disabled=no /ip dhcp-relay add name=Local2-Relay interface=Local2 \ dhcp-server=192.168.0.1 local-address=192.168.2.1 disabled=no [admin@DHCP-Relay] ip dhcp-relay> print Flags: X-disabled, I-invalid # NAME INTERFACE DHCP-SERVER LOCAL-ADDRESS 0 Local1-Relay Local1 192.168.0.1 192.168.1.1 1 Local2-Relay Local2 192.168.0.1 192.168.2.1 [admin@DHCP-Relay] ip dhcp-relay>

DHCP Relay with VRF (introduced in 7.15)

Let's take the previous setup but we'll consider that the interface to the DHCP server and interfaces to DHCP clients are added in VRF:

/ip vrf add interfaces=To-DHCP-Server name=vrf_server add interfaces=Local2 name=vrf2 add interfaces=Local1 name=vrf1

In the DHCP-relay configuration dhcp-server-vrf should be added:

/ip dhcp-relay/set dhcp-server-vrf=vrf_server numbers=0,1

Due to VRF configuration there are several routing-tables-we should add additional routes:

/ip route add disabled=no distance=1 dst-address=192.168.0.0/24 gateway=To-DHCP-Server@vrf_server pref-src="" routing- table=vrf1 scope=10 suppress-hw-offload=no \ target-scope=10 add disabled=no distance=1 dst-address=192.168.0.0/24 gateway=To-DHCP-Server@vrf_server pref-src="" routing- table=vrf2 scope=10 suppress-hw-offload=no \ target-scope=10 add disabled=no dst-address=192.168.1.0/24 gateway=Local1@vrf1 routing-table=vrf_server suppress-hw-offload=no add disabled=no distance=1 dst-address=192.168.2.0/24 gateway=Local2@vrf2 pref-src="" routing-table=vrf_server scope=30 suppress-hw-offload=no \ target-scope=10

To achieve successful DHCP-server-DHCP-relay communication we should add NAT rules:

/ip firewall nat add action=dst-nat chain=dstnat dst-address=192.168.2.1 dst-port=67 in-interface=To-DHCP-Server protocol=udp src-address=192.168.0.1 to-addresses=\

192.168.0.2 add action=dst-nat chain=dstnat dst-address=192.168.1.1 dst-port=67 in-interface=To-DHCP-Server protocol=udp src-address=192.168.0.1 to-addresses=\
192.168.0.2
## DHCPv6 Relay

Summary

Sub-menu: /ipv6 dhcp-relay

DHCPv6 Relay in RouterOS acts as an intermediary that forwards DHCPv6 client solicitations received on a local interface to a remote DHCPv6 server. The relay adds a Hop‑By‑Hop option containing its own link‑local address, enabling the server to know the client’s network location. Responses from the server are returned to the relay, which removes the Hop‑By‑Hop option and delivers the reply to the originating client. This allows a single DHCPv6 server to service multiple subnets without being directly connected to each, while preserving proper address assignment and prefix delegation. The relay requires IPv6 forwarding to be enabled and appropriate firewall allowances for UDP ports546 (client) and547 (server).

Properties

Property Description

comment (string; Default: ) Descriptive name of an item.

delay-threshold (time | none; If secs field in DHCP packet is smaller than delay-threshold, then this packet is ignored. Default: none)

dhcp-server (IPv6 address [IPv6]% A list of DHCP server IP addresses to which DHCP requests should be forwarded (optionally, the interface can interface; Default: ) also be specified together with the IPv6 address).

interface (interface; Default: ) Interface name the DHCP relay will be working on.

name (string; Default: ) Descriptive name for the relay

dhcp-options (DHCPv6 option; A list of DHCPv6 options to be inserted by the relay into forwarded DHCPv6 packets. By default, relay inserts Default: client_mac) option 79.

disabled (yes | no; Default: no) Whether relay is disabled or not. By default, it is not disabled.

link-address (IPv6 address [IPv6]; An IPv6 address that may be used by the server to identify the link on which the client is located. Defaul: :: )

store-relayed-bindings (yes | no; Inspects relayed DHCP advertisements and stores assigned prefixes. Should be used, for example, to avoid loss Default: no) of routing information on relay reboot. By default, it is disabled.

DNS

Introduction DNS configuration DNS Cache DNS Static DNS over HTTPS (DoH) Known compatible/incompatible DoH services Adlist Whitelist for Adlist Configuration examples: URL based adlist: Locally hosted adlist: Forwarders Forwarder configuration Configuration example mDNS

## Introduction

Domain Name System (DNS) usually refers to the Phonebook of the Internet. In other words, DNS is a database that links strings (known as hostnames), such as www.mikrotik.com to a specific IP address, such as 159.148.147.196.

A MikroTik router with a DNS feature enabled can be set as a DNS cache for any DNS-compliant client. Moreover, the MikroTik router can be specified as a primary DNS server under its DHCP server settings. When the remote requests are enabled, the MikroTik router responds to TCP and UDP DNS requests on port 53.

When both static and dynamic servers are set, static server entries are preferred, however, it does not indicate that a static server will always be used (for example, previously query was received from a dynamic server, but static was added later, then a dynamic entry will be preferred).

When DNS server allow-remote-requests are used make sure that you limit access to your server over TCP and UDP protocol port 53 only for known hosts.

There are several options on how you can manage DNS functionality on your LAN-use public DNS, use the router as a cache, or do not interfere with DNS configuration. Let us take as an example the following setup: ISP) → Gateway (GW) → Local area network (LAN). The GW is Internet service provider ( RouterOS based device with the default configuration:

You do not configure any DNS servers on the "GW" DHCP server network configuration-the device will forward the DNS server IP address configuration received from `ISP` to `LAN` devices; You configure DNS servers on the "GW" DHCP server network configuration-the device will give configured DNS servers to `LAN` devices (also " /ip dns set allow-remote-requests=yes" must be enabled); "dns-none" configured under DNS servers on "GW" DHCP server network configuration-the device will not forward any of the dynamic DNS servers to `LAN` devices;

### DNS configuration

DNS facility is used to provide domain name resolution for the router itself as well as for the clients connected to it.

Property Description

allow-remote-requests (yes no |; Specifies whether to allow router usage as a DNS cache for remote clients. Otherwise, only the router itself will use Default: no) DNS configuration.

address-list-extra-time (time; Extra time added to TTL when creating address list entry. Default: 0s)

cache-max-ttl (time; Default: 1w) Maximum time-to-live for cache records. In other words, cache records will expire unconditionally after cache-max- TTL time. Shorter TTLs received from DNS servers are respected.

cache-size (integer[64.. Specifies the size of the DNS cache in KiB. 4294967295]; Default: 2048)

max-concurrent-queries (integer Specifies how many concurrent queries are allowed.; Default: 100)

max-concurrent-tcp-sessions (in Specifies how many concurrent TCP sessions are allowed. teger; Default: 20)

max-udp-packet-size (integer Maximum size of allowed UDP packet. [50..65507]; Default: 4096)

mdns-repeat-ifaces (list of Once an interface in this list receives an mDNS packet, it will forward it to all other interfaces in this list. Only interfaces; Default: ) supports IPv4.

query-server-timeout (time; Specifies how long to wait for a query response from a server. Default: 2s)

query-total-timeout (time; Specifies how long to wait for query response in total. Note that this setting must be configured taking into account Default: 10s) "query-server-timeout" and the number of used DNS servers.

servers (list of IPv4/IPv6 List of DNS server IPv4/IPv6 addresses addresses@vrf; Default: )

cache-used (integer) Shows the currently used cache size in KiB

dynamic-server (IPv4/IPv6 list) List of dynamically added DNS servers from different services, for example, DHCP.

doh-max-concurrent-queries (int Specifies how many DoH concurrent queries are allowed. eger; Default: 50)

doh-max-server-connections (int Specifies how many concurrent connections to the DoH server are allowed. eger; Default: )5

doh-timeout (time; Default: 5s) Specifies how long to wait for query response from the DoH server.

use-doh-server (string; Default: ) Specified which DoH server must be used for DNS queries. DoH functionality overrides "servers" usage if specified. The server must be specified with an "https://" prefix. Supports only one DoH server.

verify-doh-cert  (yes no |; Specifies whether to validate the DoH server, when one is being used. Will use the "/certificate" list in order to verify Default: no) server validity.

vrf (vrf; Default: main) Specifies the VRF that should use the DNS resolver. The DNS resolver processes only requests originating from the designated VRF or from the resolver itself.

[admin@MikroTik] > ip dns print servers: dynamic-servers: 10.155.0.1 use-doh-server: verify-doh-cert: no doh-max-server-connections: 5 doh-max-concurrent-queries: 50 doh-timeout: 5s allow-remote-requests: yes max-udp-packet-size: 4096 query-server-timeout: 2s query-total-timeout: 10s max-concurrent-queries: 100 max-concurrent-tcp-sessions: 20 cache-size: 2048KiB cache-max-ttl: 1d cache-used: 48KiB

Dynamic DNS servers are obtained from different facilities available in RouterOS, for example, DHCP client, VPN client, IPv6 Router Advertisements, etc.

Servers are processed in a queue order-static servers as an ordered list, dynamic servers as an ordered list. When DNS cache has to send a request to the server, it tries servers one by one until one of them responds. After that this server is used for all types of DNS requests. Same server is used for any types of DNS requests, for example, A and AAAA types. If you use only dynamic servers, then the DNS returned results can change after reboot, because servers can be loaded into IP/DNS settings in a different order due to a different speeds on how they are received from facilities mentioned above.

If at some point the server which was being used becomes unavailable and can not provide DNS answers, then the DNS cache restarts the DNS server lookup process and goes through the list of specified servers once more.

### DNS Cache

This menu provides two lists with DNS records stored on the server:

"/ip dns cache : this menu provides a list with cache DNS entries that RouterOS cache can reply with t " o client requests; "/ip dns cache all : This menu provides a complete list with all cached DNS records stored including a " lso, for example, PTR records.

You can empty the DNS cache with the command: "/ip dns cache flush".

### DNS Static

The MikroTik RouterOS DNS cache has an additional embedded DNS server feature that allows you to configure multiple types of DNS entries that can be used by the DNS clients using the router as their DNS server. This feature can also be used to provide false DNS information to your network clients. For example, resolving any DNS request for a certain set of domains (or for the whole Internet) to your own page.

[admin@MikroTik] /ip dns static add name=www.mikrotik.com address=10.0.0.1

The server is also capable of resolving DNS requests based on basic regular expressions so that multiple requests can be matched with the same entry. In case an entry does not conform with DNS naming standards, it is considered a regular expression. The list is ordered and checked from top to bottom. Regular expressions are checked first, then the plain records.

Use regex to match DNS requests:

[admin@MikroTik] /ip dns static add regexp="[*mikrotik*]" address=10.0.0.2

If DNS static entries list matches the requested domain name, then the router will assume that this router is responsible for any type of DNS request for the particular name. For example, if there is only an "A" record in the list, but the router receives an "AAAA" request, then it will reply with an "A" record from the static list and will query the upstream server for the "AAAA" record. If a record exists, then the reply will be forwarded, if not, then the router will reply with an "ok" DNS reply without any records in it. If you want to override domain name records from the upstream server with unusable records, then you can, for example, add a static entry for the particular domain name and specify a dummy IPv6 address for it "::ffff".

List all of the configured DNS entries as an ordered list:

[admin@MikroTik] /ip/dns/static/print Columns: NAME, REGEXP, ADDRESS, TTL # NAME REGEXP ADDRESS TTL 0 www.mikrotik.com 10.0.0.1 1d 1 [*mikrotik*] 10.0.0.2 1d

Property Description

address (IPv4/IPv6) The address that will be used for "A" or "AAAA" type records.

cname (string) Alias name for a domain name.

forward-to The IP address of a domain name server to which a particular DNS request must be forwarded.

mx-exchange (string) The domain name of the MX server.

name (string) Domain name.

|srv-port (integer; Default: )||0||The TCP or UDP port on which the service is to be found.|
|---|---|---|---|---|
|srv-target||||The canonical hostname of the machine providing the service ends in a dot.|
|text (string)||||Textual information about the domain name.|
|type (A|| AAAA | CNAME|| FWD | MX NS N|| ||Type of the DNS record.|
|XDOMAIN SRV TXT address-list (string) comment (string)|| ||; Default: A)||Name of the Firewall address list to which address must be dynamically added when some request matches the entry. Entry will be removed from the address list when TTL expires. Comment about the domain name record.|
|disabled (yes no||; Default: yes)|||Whether the DNS record is active.|
|match-subdomain (yes no|||; Default: no)||Whether the record will match requests for subdomains.|
|mx-preference (integer; Default: ) ns (string) regexp (regex)||0||Preference of the particular MX record. Name of the authoritative domain name server for the particular record. Regular expression against which domain names should be verified.|
|srv-priority (integer; Default: )||0||Priority of the particular SRV record.|
|srv-weight (integer; Default: ) ttl (time; Default: 24h)||0||Weight of the particular SRV record. Maximum time-to-live for cached records.|

For each static A and AAAA record, in cache automatically is added a PTR record.

Regexp is case-sensitive, but DNS requests are not case sensitive, RouterOS converts DNS names to lowercase before matching any static entries. You should write regex only with lowercase letters. Regular expression matching is significantly slower than plain text entries, so it is advised to minimize the number of regular expression rules and optimize the expressions themselves.

Be careful when you configure regex through mixed user interfaces-CLI and GUI. Adding the entry itself might require escape characters when added from CLI. It is recommended to add an entry and the execute print command in order to verify that regex was not changed during addition.

## DNS over HTTPS (DoH)

RouterOS support DNS over HTTPS (DoH). DoH uses HTTPS protocol to send and receive DNS requests for better data integrity. The main goal is to provide privacy by eliminating "man-in-the-middle" attacks (MITM).

Video: DoH setup

It is strongly recommended to import the root CA certificate of the DoH server you have chosen to use for increased security. We strongly suggest not using third-party download links for certificate fetching. Use the Certificate Authority's own website.

There are various ways to find out what root CA certificate is necessary. The easiest way is by using your WEB browser, navigating to the DoH site, and checking the security of the website. You can download the certificate straight from the browser or fetch the certificate from a trusted source.

Download the certificate, upload it to your router and import it:

/certificate import file-name=CertificateFileName

Configure the DoH server:

/ip dns set use-doh-server=DoH_Server_Query_URL verify-doh-cert=yes

Only one DoH server is supported.

Note that you need at least one regular DNS server configured for the router to resolve the DoH hostname itself.

/ip dns set servers=1.1.1.1

If you do not have any dynamical or static DNS server configured, add a static DNS entry for the DoH server domain name like this:

/ip dns static add address=IP_Address name=Domain_Name

If DoH server is being used (DoH DNS name can be resolved) then it will be the only DNS service working at the time and standard DNS servers from IP/DNS servers list will not be used.

If /certificate/settings/set crl-use is set to yes, RouterOS will check CRL for each certificate in a certificate chain, therefore, an entire certificate chain should be installed into a device-starting from Root CA, intermediate CA (if there are such), and certificate that is used for specific service.

For example, Google DoH, Cloudflare, and OpenDNS full chain contain three certificates,  NextDNS has four certificates.

### Known compatible/incompatible DoH services

Compatible DoH services:

Cloudflare Google NextDNS OpenDNS

Incompatible DoH services:

Mullvad Yandex UncensoredDNS Quad9 (due to their migration to HTTP2 which is not currently supported in RouterOS)

## Adlist

Adlist is an integral component of network-level ad blocking, comprising a curated collection of domain names known for serving advertisements. This feature operates by utilizing Domain Name System (DNS) resolution to intercept A and AAAA requests to these domains. When a client device queries a DNS server for a domain listed on the adlist, the DNS resolution process is altered. Instead of returning the actual IP address of the ad-serving domain, the DNS server responds with the IP address 0.0.0.0. This effectively null-routes the request, as 0.0.0.0 is a non-routable meta-address used to denote an invalid, unknown, or non-applicable target. By redirecting ad-related requests in this manner, the adlist feature ensures that advertisement content is not loaded, enhancing network performance and improving the user experience by reducing unwanted ad traffic.

Video: Adlist setup

Before configuring, increase the DNS cache as it's used to store adlist entries. If limit is reached and error in DNS,error topic is printed "adlist read: max cache size reached"

Adlist is stored on device's internal memory. Ensure that there is enough free space to save the desired adlist.

Property Description

url Used to specify the URL of an adlist.

ssl-verify Specifies whether to validate the SSL certificate of the Adlist URL server.   Will use the "/certificate" list to verify server validity.

match-Count of matched DNS name requests. count

name-Count of DNS names imported from the Adlist. count

file Used to specify a local file path from which to read adlist data.

pause Temporarily pause the use of all adlist.

reload Checks for updates for all lists, if updates are found, the list is updated, removing or adding entries as needed, the lists are not redownloaded in whole when issuing a reload, instead only necessary updates are done.

It's not mandatory to use reload to update the lists, Adlist checks for new updates once every four hours.

### Whitelist for Adlist

To exempt certain domains from Adlist, you need to create a static DNS FWD entry, for example, /ip/dns/static/add name=bar.test type=FWD, if such entry is present, the query will be answered by the router if it has relevant static DNS entry /ip/dns/static/add name=bar.test type=A, or alternatively, if no static rule is present, forwarded to the next DNS, either dynamic or one configured under "/ip/dns/set servers=", FWD entries are supported by DoH as well.

### Configuration examples:

URL based adlist:

/ip/dns/adlist add url=https://raw.githubusercontent.com/StevenBlack/hosts/master/hosts ssl-verify=no

To see how many domain names are present and matched, you can run:

/ip/dns/adlist/print Flags: X-disabled 0 url="https://raw.githubusercontent.com/StevenBlack/hosts/master/hosts" ssl-verify=no match-count=122 name- count=164769

Locally hosted adlist:

To create your adlist, you can create a Txt file with the domains. Example:

0.0.0.0 example1.com
0.0.0.0 eu1.example.com
0.0.0.0 ex.com
0.0.0.0 com.example.com You can create the txt file on your PC, but it is also possible to create it in RouterOS, with following commands "/file/add name=host.txt", and then you can run "file/edit host.txt contents" after adding entries, press "ctrl o" to save the entries.

|To add file to adlist :|||
|---|---|---|
||/ip/dns/adlist/add file=host.txt|You can verify that file is formatted correctly with "/ip/dns/adlist/print" ,the results will show how many hostnames you have added, the hostname format must match the format given in previous example.|
|/ip/dns/adlist/print Flags: X-disabled||0 file=host.txt match-count=0 name-count=4|
|Forwarders|Forwarder configuration|DNS Forwarders allows a user to configure a named DNS forwarder that can be used for static FWD entries as forward-to value. For each Forwarder is possible to configure multiple regular upstream and DoH servers. Configured forwarder servers will be used by round-robin algorithm-for each query, next server will be used to resolve DNS name. In /ip/dns/forwaders section, forwarders can added, modified or removed.|
|Property||Description|
|name (string; Default: ) dns-servers (string; Default:) doh-servers (string; Default:) verify-doh-cert (yes no Default: yes) Configure/add a forwarder:||; Configuration example|Forwarder name. An IP address or DNS name of a domain name server. Can contain multiple records, for example, dns-servers=1. 1.1.1,8.8.8.8,local.dns A URL of DoH server. Can contain multiple records. Specifies whether to validate the DoH server, when one is being used. Will use the "/certificate" list in order to verify server validity.|
|/ip dns forwarders|Configure/add a statis DNS FWD entry:|add dns-servers=1.1.1.1,local.dns doh-servers=https://dns.google/dns-query name=forwarder1|
|/ip dns static||add forward-to=forwarder1 name=mikrotik.com type=FWD|
|gle DoH server.||Now each time when a router will receive request to resolve mikrotik.com, request using round-robin algorithm will be forwarded to 1.1.1.1 local.dns, or Goo|

mDNS

RouterOS supports Multicast DNS (mDNS) for local network service discovery. By default, mDNS operates within a single subnet. The mDNS repeater feature allows to extend mDNS functionality across different interfaces or VLANs using the "mdns-repeat-ifaces" property.

Impact of using mDNS Repeater:

Cross-Subnet Service Discovery: Devices on different subnets or VLANs can discover each other, enhancing the ability to find services (e.g., printers, file sharing); Increased Network Traffic: mDNS repeater may increase multicast traffic, which could lead to congestion, especially in larger networks with many devices.

The mDNS repeater is commonly used with devices such as:

Apple Ecosystem (AirPrint, AirPlay); Smart Home Devices (Thread, IoT); Chromecast and Media Streaming; Avahi (Linux/Unix).

To enable the mDNS repeater between interfaces, allowing devices connected to these interfaces to discover each other using mDNS, use the following command:

/ip dns set mdns-repeat-ifaces=<interface1>,<interface2>

mDNS repeater requires multicast-capable interfaces (e.g., Ethernet, VLAN, bridge). Tunnel interfaces such as WireGuard are not supported.

Currently only IPv4 is supported.

MikroTik mDNS Repeater is a local service intercepting multicast packets to rebroadcast them, it requires an "input" rule. mDNS multicast traffic does not traverse the "forward" chain. In case you have strict firewall rules protecting your router from local subnets, you must explicitly allow mDNS traffic before any drop-allowed to receive UDP port 5353 traffic on the "input" chain.
