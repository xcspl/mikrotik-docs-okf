---
type: Reference
title: "OpenVPN"
description: "The OpenVPN security model is based on SSL, the industry standard for secure communications via the internet. OpenVPN implements OSI layer 2 or 3 secure network extensions using the SSL/TLS protocol. Support IPv4, IPv6."
timestamp: '2026-10-06'
status: active
tags: [routeros, mikrotik, networking]
resource: ~/Downloads/ROS-260526-1445-796.pdf
sources:
  - resource: https://manual.mikrotik.com/docs/introduction/
---

# OpenVPN

Overview Introduction Limitations OVPN Client Tls-crypt, tls-crypt v2 OVPN Server Server Configuration Properties Example Setup Overview Creating Certificates Server Config Client Config Push Route VRF support

## Overview

The OpenVPN security model is based on SSL, the industry standard for secure communications via the internet. OpenVPN implements OSI layer 2 or 3 secure network extensions using the SSL/TLS protocol. Support IPv4, IPv6.

## Introduction

OpenVPN has been ported to various platforms, including Linux and Windows, and its configuration is likewise on each of these systems, so it makes it easier to support and maintain. OpenVPN can run over User Datagram Protocol (UDP) or Transmission Control Protocol (TCP) transports, multiplexing created SSL tunnels on a single TCP/UDP port. OpenVPN is one of the few VPN protocols that can make use of a proxy, which might be handy sometimes.

## Limitations

ROS has its own ovpn implementation, not all ovpn features are supported and not all unsupported are listed. Currently, noteable unsupported OpenVPN features:

LZO compression. **DEPRECATED** Compression is generally not recommended. VPN tunnels which use compression are susceptible to the VORALCE attack vector. NCP autonegotiation, cipher has to been specified in .ovpn file when connecting to an ROS ovpn server.

OpenVPN username is limited to 27 characters and the password to 233 characters. Password cap increased in 7.18_ab253 to 1000 characters.

## OVPN Client

Property Description

|add-default-route (yes no||||; Default: no)||Whether to add OVPN remote address as a default route.|
|---|---|---|---|---|---|
|auth (md5 sha1 null sha256 sha512|||||||; Default: sha1)|Allowed authentication methods.|
|certificate (string none||||; Default: none)||Name of the client certificate|
|cipher (null aes128-cbc aes128-gcm aes192-cbc aes192-gcm||||||||| Allowed ciphers. In order to use GCM type ciphers, the "auth" parameter must|
|aes256-cbc aes256-gcm blowfish128 comment (string; Default: ) connect-to (IP|IPv6; Default: )||||||; Default: blowfish128)|be set to "null", because GCM cipher is also responsible for "auth", if used. Descriptive name of an item Remote address of the OVPN server.|

|

|

||disabled (yes no | mac-address (MAC; Default:) max-mtu (integer; Default: 1500) mode (ip ethernet | name (string; Default:) password (string; Default:) port (integer; Default: 1194) profile (name; Default: default) protocol (tcp  udp | verify-server-certificate (yes no tls-version (any   only-1.2 | use-peer-dns (yes no | | route-nopull (yes no user (string; Default:)|; Default: yes); Default:) ""; Default: tcp)|ip sensitive |; Default: no); Default: any); Default: no); Default: no) already includes configuration so you need to worry only about a few parameters.|Whether the interface is disabled or not. By default it is disabled. Mac address of OVPN interface. Will be automatically generated if not specified. Maximum Transmission Unit. Max packet size that the OVPN interface will be able to send without packet fragmentation. Layer3 or layer2 tunnel mode (alternatively tun, tap) Descriptive name of the interface. Password used for authentication. Value of password should not be longer than 1000 chars. Port to connect to. Specifies which PPP profile configuration will be used when establishing the tunnel. indicates the protocol to use when connecting with the remote endpoint. Checks the certificates CN or SAN against the "connect-to" parameter. The IP or hostname must be present in the server's certificate. Specifies which TLS versions to allow Whether to add DNS servers provided by the OVPN server to IP/DNS configuration. Specifies whether to allow the OVPN server to add routes to the OVPN client instance routing table. User name used for authentication. Also, it is possible to import the OVPN client configuration from a .ovpn configuration file. Such a file usually is provided from the OVPN server side and /interface/ovpn-client/import-ovpn-configuration ovpn-password=securepassword \ key-passphrase=certificatekeypassphrase ovpn-user=myuserid skip-cert-import=no|
|---|---|---|---|---|
||||you generate a shared-secret key, this key should be added to the client configuration file .ovpn.|OVPN client supports tls authentication. The configuration of tls-auth can be added only by importing .ovpn configuration file. Using tls-auth requires that Note* ROS client requires user name and password. Authentication is managed by server side, if its supports tls, then user name will be ignored.|
|<tls-auth> # # </tls-auth>|key-direction 1 # 2048 bit OpenVPN static key|-----BEGIN OpenVPN Static key V1----- -----END OpenVPN Static key V1-----|7.17beta5 added support to allow non-null auth in gcm mode.||
||Tls-crypt, tls-crypt v2||To improve TLS auth, Tls-crypt is added in version 7.17rc3. Tls-crypt, tls-crypt v2 is suppoorted only for ovpn client with following settings: “auth SHA256” and no key-direction in server configuration,||

“auth SHA256” and “key-direction 1” in client configuration is needed for authentication to work.

Example configuration files:

client-1.ovpn

server-1.conf

## OVPN Server

/interface ovpn-server

An interface is created for each tunnel established to the given server. There are two types of interfaces in the OVPN server's configuration

Static interfaces are added administratively if there is a need to reference the particular interface name (in firewall rules or elsewhere) created for the particular user. Dynamic interfaces are added to this list automatically whenever a user is connected and its username does not match any existing static entry (or in case the entry is active already, as there can not be two separate tunnel interfaces referenced by the same name).

Dynamic interfaces appear when a user connects and disappear once the user disconnects, so it is impossible to reference the tunnel created for that use in router configuration (for example, in the firewall), so if you need a persistent rule for that user, create a static entry for him/her. Otherwise, it is safe to use dynamic configuration.

After upgrade to 7.17 version ovpn server will receive its configuration, due to multiple server support.

An disabled ovpn server with added mac will appear in configuration: /interface ovpn-server server add mac-address=99:99:99:99:99:99 name=ovpn-server1

In both cases PPP users must be configured properly-static entries do not replace PPP configuration.

### Server Configuration

Properties

|Property||||Description|
|---|---|---|---|---|
|auth (md5 sha1 null sha256 sha512 a1,md5,sha256,sha512)|| ||| ||; Default: sh|Authentication methods that the server will accept.|
|certificate (name none|||; Default: none)||Name of the certificate that the OVPN server will use.|
|cipher (null aes128-cbc aes128-gcm aes192-cbc|||||||Allowed ciphers.|
|| aes192-gcm aes256-cbc aes256-gcm blowfish1 28; Default: aes128-cbc,blowfish128)||||||||
|default-profile (name; Default: default)||||Default profile to use.|
|disabled (yes no||; Default: yes)|||Defines whether the OVPN server is enabled or not.|
|protocol (tcp | udp; Default: tcp)||||Indicates the protocol to use when connecting with the remote endpoint.|
|keepalive-timeout (integer disabled||||; Default: 60)|Defines the time period (in seconds) after which the router is starting to send keepalive packets every second. If no traffic and no keepalive responses have come for that period of time (i.e. 2 * keepalive-timeout), not responding client is proclaimed disconnected|
|mac-address (MAC; Default: )||||Automatically generated MAC address of the server.|
|max-mtu (integer; Default: 1500)||||Maximum Transmission Unit. Max packet size that the OVPN interface will be able to send without packet fragmentation.|

mode (ip ethernet |; Default: ) ip

name (string)

netmask (integer; Default: 24)

port (integer; Default: 1194)

require-client-certificate (yes no |; Default: no)

redirect-gateway (def1 disabled ipv6; | | Default: disa bled)

enable-tun-ipv6 (yes no; | Default: no)

ipv6-prefix-len (integer; Default: 64)

reneg-sec  (integer; Default: 3600)

push-routes (string; Default: )

tls-version (any |only-1.2; Default: any )

tun-server-ipv6 (IPv6 prefix; Default: )::

user-auth-method (mschap2 | pap; Default pap)

vrf ()

required client certificate to export work.

Layer3 or layer2 tunnel mode (alternatively tun, tap)

Name of the server

Subnet mask to be applied to the client.

Port to run the server on.

If set to yes, then the server checks whether the client's certificate belongs to the same certificate chain.

Specifies what kind of routes the OVPN client must add to the routing table.

def1 – Use this flag to override the default gateway by using 0.0.0.0/1 and 128.0.0.0/1 rather than 0.0.0.0/0. This has the benefit of overriding but not wiping out the original default gateway. disabled-Do not send redirect-gateway flags to the OVPN client. ipv6 - Redirect IPv6 routing into the tunnel on the client side. This works similarly to the def1 flag, that is, more specific IPv6 routes are added (2000::/4 and 3000::/4), covering the whole IPv6 unicast space.

Specifies if IPv6 IP tunneling mode should be possible with this OVPN server.

Length of IPv6 prefix for IPv6 address which will be used when generating OVPN interface on the server side.

Key renegotiate seconds, the time the server periodically renegotiates the secret key for the data channel.

Push route support are added in 7.14, the maximum of possible input is limited to 1400 characters or 37 pushed routes. IPv6 support added in 7.21_ab220.

TLS protocol setting.

IPv6 prefix address which will be used when generating the OVPN interface on the server side.

By the default pap authentication method is used, if preferred server authentication with chap challenge set mschap2 in server settings.

VRF in which listen for connection attempts

## Example

### Setup Overview

Also, it is possible to prepare a .ovpn file for the OVPN client which can be easily imported on the end device. Server need to have option enabled -

interface/ovpn-server/server/export-client-configuration ca-certificate=ca.crt client-certificate=cert_e xport_rw-client.crt client-cert-key=cert_export_rw-client.key server-address=1.1.1.1 server=ovpn-server1

It is very important that the date on the router is within the range of the installed certificate's date of expiration. To overcome any certificate verification problems, enable NTP date synchronization on both the server and the client.

Assume that Office public IP address is 2.2.2.2 and we want two remote OVPN clients to have access to 10.5.8.20 and 192.168.55.0/24 networks behind the office gateway.

### Creating Certificates

All certificates can be created on the RouterOS server using the certificate manager. See example >>.

For the simplest setup, you need only an OVPN server certificate.

### Server Config

The first step is to create an IP pool from which client addresses will be assigned and some users.

/ip pool add name=ovpn-pool range=192.168.77.2-192.168.77.254

/ppp profile add name=ovpn local-address=192.168.77.1 remote-address=ovpn-pool /ppp secret add name=client1 password=123 profile=ovpn add name=client2 password=234 profile=ovpn

Assume that the server certificate is already created and named "server"

/interface ovpn-server server add disabled=no certificate=server name=myServer

### Client Config

Add manually which networks you want to access over the tunnel.

/interface ovpn-client add name=ovpn-client1 connect-to=2.2.2.2 user=client1 password=123 disabled=no /ip route add dst-address=10.5.8.20 gateway=ovpn-client1 add dst-address=192.168.55.0/24 gateway=ovpn-client1 /ip firewall nat add chain=srcnat action=masquerade out-interface=ovpn-client1

### Push Route

Push route support are added in 7.14, the maximum of possible input is limited to 1400 characters or 37 routes. IPv6 support added in 7.21_ab220. example: route network/IP [netmask] [gateway] [metric].

/interface ovpn-server server set myServer push-routes="192.168.102.0 255.255.255.0 192.168.109.1 9"

/interface/ovpn-server/server/set push-routes-ipv6="fdaa::/64,2001:db8::/32" 0

### VRF support

Support starting from 7.17 version is added, and couple changes introduced in configuration, if you use latest version, please refer to this example:

Server side configuration:

/interface ovpn-server server add disabled=no certificate=yourcert auth=sha1 cipher=aes128-cbc require-client-certificate=yes protocol=tcp name=ovpn-server1 vrf=main
