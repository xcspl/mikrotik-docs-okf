---
type: Reference
title: "Services"
description: "IP/Services lists the protocols and ports used by various MikroTik RouterOS services and containers, including those for incoming connections."
timestamp: '2026-05-26'
status: active
tags: [routeros, mikrotik, networking]
resource: ~/Downloads/ROS-260526-1445-796.pdf
sources:
  - resource: https://help.mikrotik.com/docs/spaces/ROS/pages/328059/RouterOS
---

# Services

Summary Properties Read-only properties Example Protocols and ports Web server

## <u>Summary</u>

IP/Services lists the protocols and ports used by various MikroTik RouterOS services and containers, including those for incoming connections.

It helps to determine which MikroTik services (or containers) are listening on specific ports, and what needs to be blocked or allowed if you want to restrict or permit access to certain services.

The default services that can be configured from IP/Services section:

Property Description

telnet Telnet service

ftp FTP service

www WebFig HTTP service

ssh SSH service

www-ssl WebFig HTTPS service

api API service

winbox Responsible for WinBox tool access, as well as MikroTik smartphone app and Dude

api-ssl API over SSL service

reverse-proxy Reverse Proxy service

## <u>Properties</u>

Note that it is not possible to add new services, only existing service modifications are allowed.

Sub-menu: /ip service

Property Description

address (IP address List of IP/IPv6 prefixes from which the service is accessible. When this parameter is set, packets are not dropped at the /netmask | IPv6/0..128; network level, but access to the service is denied for sources not matching the specified addresses. Default: ) This option is best suited for restricting access within trusted networks.

To block access from external or untrusted networks, we recommend using a Firewall instead.

certificate (name; Default: n The name of the certificate used by a particular service. Applicable only for services that depend on certificates (www- one) ssl, api-ssl)

name (name; Default: none) Service name

max-sessions (integer: 1.. Max simultaneous session count for service 1000; Default: 20)

port (integer: 1..65535; The port particular service listens on Default: )

tls-version (any | only-1.2; Specifies which TLS versions to allow by a particular service Default: any)

vrf (name; Default: main) Specify which VRF instance to use by a particular service

### Read-only properties

Property Description

Container Name of the container listening on the port

Local Router local address used for the connection

Remote Remote address that established the connection to the service

Example

For example, allow API only from a specific IP/IPv6 address range

[admin@dzeltenais_burkaans] /ip/service/set api address=10.5.101.0/24,2001:db8:fade::/64 [admin@dzeltenais_burkaans] /ip/service/print where !dynamic Flags: X-DISABLED, I-INVALID Columns: NAME, PORT, PROTO, ADDRESS, CERTIFICATE, VRF, MAX-SESSIONS # NAME PORT PROTO ADDRESS CERTIFICATE VRF MAX-SESSIONS 0 ftp 21 tcp main 20 1 ssh 22 tcp main 20 2 telnet 23 tcp main 20 7 www 80 tcp main 20 9 X www-ssl 443 tcp none main 20 13 winbox 8291 tcp main 20 15 api 8728 tcp 10.5.101.0/24 main 20 2001:db8:fade::/64 16 api-ssl 8729 tcp none main 20

Example that shows dynamic services that listens or has establish connections to router services

[admin@dzeltenais_burkaans] /ip/service/print where dynamic Flags: D-DYNAMIC; c-CONNECTION Columns: NAME, NETNS, CONTAINER, PORT, PROTO, LOCAL, REMOTE # NAME NETNS CONTAINER PORT PROTO LOCAL REMOTE 3 D resolver 53 tcp 4 D resolver 53 udp 5 D dhcp 67 udp 6 D dhcpclient 68 udp 8 D snmp 161 udp 10 D btest 2000 tcp 11 D loader 3986 tcp 12 D discover 5678 udp 14 Dc winbox 8291 tcp 10.155.221.4 10.145.221.15:51595 17 D pihole-FTL 16 Pi-hole 53 tcp 18 D pihole-FTL 16 Pi-hole 53 udp 19 D lighttpd 16 Pi-hole 80 tcp 28 Dc lighttpd 16 Pi-hole 80 tcp 172.55.1.2 10.145.221.15:52298 29 Dc lighttpd 16 Pi-hole 80 tcp 172.55.1.2 10.145.221.15:52333 30 Dc lighttpd 16 Pi-hole 80 tcp 172.55.1.2 10.145.221.15:52339 31 Dc lighttpd 16 Pi-hole 80 tcp 172.55.1.2 10.145.221.15:52340 32 Dc lighttpd 16 Pi-hole 80 tcp 172.55.1.2 10.145.221.15:52341 33 Dc lighttpd 16 Pi-hole 80 tcp 172.55.1.2 10.145.221.15:52342 26 D pihole-FTL 16 Pi-hole 4711 tcp

## <u>Protocols and ports</u>

The table below shows the list of protocols and ports used by RouterOS.

Proto/Port

20/tcp

21/tcp

22/tcp

23/tcp

53/tcp 53/udp

67/udp

68/udp

80/tcp

123/udp

161/udp

179/tcp

443/tcp

500/udp

520/udp 521/udp

546/udp

547/udp

646/tcp

646/udp

1080/tcp

1698/udp 1699/udp

1701/udp

1723/tcp

1900/udp 2828/tcp

1966/udp

1966/tcp

2000/tcp

5246,5247/udp

5350/udp

5351/udp

5678/udp

6343/tcp

Description

FTP data connection

FTP control connection

Secure Shell (SSH) remote login protocol

Telnet protocol

DNS

Bootstrap protocol or DHCP Server

Bootstrap protocol or DHCP Client

World Wide Web HTTP

Network Time Protocol (NTP)

Simple Network Management Protocol (SNMP)

Border Gateway Protocol (BGP)

Secure Socket Layer (SSL) encrypted HTTP

Internet Key Exchange (IKE) protocol

RIP routing protocol

DHCPv6 Client message

DHCPv6 Server message

LDP transport session

LDP hello protocol

SOCKS proxy protocol

RSVP TE Tunnels

Layer 2 Tunnel Protocol (L2TP)

Point-To-Point Tunneling Protocol (PPTP)

Universal Plug and Play (uPnP)

MME originator message traffic

MME gateway protocol

Bandwidth test server

CAPsMAN

NAT-PMP client

NAT-PMP server

Mikrotik Neighbor Discovery Protocol

Default OpenFlow port

|8080/tcp|HTTP Web Proxy||
|---|---|---|
|8291/tcp|Winbox||
|8728/tcp|API||
|8729/tcp|API-SSL||
|20561/udp|MAC winbox||
|/1|ICMP||
|/2|Multicast | IGMP||
|/4|IPIP encapsulation||
|/41|IPv6 (encapsulation)||
|/46|RSVP TE tunnels||
|/47|General Routing Encapsulation (GRE) - used for PPTP and|EoIP tunnels|
|/50|Encapsulating Security Payload for IPv4 (ESP)||
|/51|Authentication Header for IPv4 (AH)||
|/89|OSPF routing protocol||
|/103|Multicast | PIM||
|/112|VRRP||

## <u>Web server</u>

The table below shows the list of properties that can be enabled/disabled for web services. All of properties are enabled by default and can be disabled if desired.

In this table "plain" refers to HTTP connections and "secure" to HTTPS connections.

Property Description

index-plain: (Default: yes) Home page/login page (Can be disabled when webfig-plain and graphs-plain are disabled)

webfig-plain: (Default: yes) WebFig interface

graphs-plain: (Default: yes) Graph page

rest-plain: (Default: yes) REST API support

crl-plain: (Default: yes) CRL()Certificate Revocation List

scep-plain: (Default: yes) SCEP(Simple Certificate Enrollment Protocol)

acme-plain: (Default: yes) ACME Challenge

index-secure: (Default: yes) Home page/login page (Can be disabled when webfig-secure and graphs-secure are disabled)

webfig-secure: (Default: yes) WebFig interface

graphs-secure: (Default: yes) Graph page

rest-secure: (Default: yes) REST API support
