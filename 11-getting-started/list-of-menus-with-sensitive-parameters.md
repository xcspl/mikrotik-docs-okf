---
type: Reference
title: "List of menus with sensitive parameters"
description: "Below you can find a list of menus where sensitive (shown only when show-sensitive parameter is used or alternatively hidden when \"Hide password\" is enabled in WinBox settings) parameters can be configured. For more deta."
timestamp: '2026-05-26'
status: active
tags: [routeros, mikrotik, networking]
resource: ~/Downloads/ROS-260526-1445-796.pdf
sources:
  - resource: https://help.mikrotik.com/docs/spaces/ROS/pages/328059/RouterOS
---

# List of menus with sensitive parameters

Below you can find a list of menus where sensitive (shown only when show-sensitive parameter is used or alternatively hidden when "Hide password" is enabled in WinBox settings) parameters can be configured. For more detailed information, please refer to the corresponding menu documentation pages.

|enabled in WinBox settings) parameters can be configured. For more detailed information, please refer to the corresponding menu documentation pages.|||
|---|---|---|
|Menu|Parameter names|Page link|
|container|password|Container#Containerconfiguration|
|ip/hotspot|password, otp-secret|HotSpot-Captive portal#HotSpotUsers|
|iot|password, key|password-MQTT#Brokers key-General Properties#Servers|
|interface/gre and|ipsec-secret|GRE#Properties|
|interface/gre6|||
|interface/ipip and|ipsec-secret|IPIP#Properties|
|interface/ipipv6|||
|interface/eoip and inter|ipsec-secret|EoIP#PropertyDescription|
|face/eoipv6|||
|interface/6to4|ipsec-secret|6to4#6to4-PropertyDescription|
|interface/ppp-client|password, pin|Work in Progress PPP|
|interface/sstp-client|password|SSTP#Properties|
|interface/l2tp-server,|ipsec-secret, password|ipsec-secret, password-L2TP#L2TPCli|
|interface/l2tp-client||ent|
|and interface/l2tp-|||
|ether||ipsec-secret-L2TP#L2TPServer ipsec-secret-L2TP#L2TPEther|
|interface/ovpn-client|password|OpenVPN#OVPNClient|
|interface/pptp-client|password|PPTP#PPTPClient|
|interface/pppoe-client|password|PPPoE#PPPoEClient|
|ppp/secret|password|PPP AAA#UserDatabase|
|ppp/l2tp-secret|secret|Work in Progress|
|ip/ssh/export-host-key|passphrase|SSH#SSHServer|
|and ip/ssh/import-host-|||
|key|||
|ip/ipsec|auth-key, enc-key, ppk-secret, secret, password, passphrase, key|auth-key, enc-key-IPsec#InstalledSAs secret, password-IPsec#Identities ppk-secret-Work in Progress IPsec#Pe|
|||ers key, passphrase-Work in Progress IPs ec#Keys|
|system/ssh-exec|password|SSH#SSHexec|
|user|password, passphrase|User|

nvme-tcp-server-password, nvme-tcp-password, smb-server-password, smb- disk password, self-encryption-password, encryption-key, sshfs-password

interface/vrrp

interface/dot1x

interface/macsec

interface/wireguard

interface/lte

socks/users

ip/cloud

ip/smb

password

radius

routing

snmp/community

system/backup

system/ntp/key

system/swos /password

system/package/local- update

system/license

tool/romon

tool/sms

tool/email

tr069-client

password

password

cak

private-key, preshared-key, *show-client-config

pin, password

password

vpn-private-key, vpn-peer-private-key, private-key

password

old-password, new-password, confirm-new-password

secret

password, tcp-md5-key, auth-key

nvme-tcp-server-password, nvme-tcp- password-ROSE- storage#NVMEoverTCP

smb-server-password, smb-password-ROSE-storage#SMB

self-encryption-password, encryption- key-ROSE-storage#Self- EncryptionDrives

sshfs-password-Work in Progress

VRRP#Parameters

Dot1X#Client

MACsec#PropertyReference

WireGuard

LTE/5G#LTEClient

Work in Progress SOCKS

Back To Home#Propertyreference

SMB#Usersetup

Password change command; no dedicated documentation page available.

RADIUS#RADIUSClient

password - /routing/rip

tcp-md5-key - /routing/bgp#/routing /bgp-/routing/bgp/connection

auth-key - /routing/ospf#/routing/ospf- /routing/ospf/interface-template

SNMP#CommunityProperties

Backup

Work in Progress NTP

SwOS password change command; no dedicated documentation page available.

Packages#LocalUpdate

RouterOS license keys#CHRLicenseLevels

RoMON#Configuration

SMS#Receiving

E-mail

TR-069#ConfigurationSettings

authentication-password, encryption-password

password

key-val

new-password, confirm-new-password

password

password

secrets

sim-pin, secret

password

connection-request-password, password

user-manager web-private-password, paypal-password, shared-secret, password, otp-secret shared-secret-User Manager#Routers

paypal-password, web-private- password-User Manager#Advanced

password, otp-secret-User Manager#Users

interface/wifi passphrase, eap-password WiFi#SecurityProperties

caps-man private-passphrase, passphrase private-passphrase-CAPsMAN#CAPs MANAccess-list

passphrase-CAPsMAN#CAPsMANco nfiguration

interface/wireless static-key-0, static-key-1, static-key-2, static-key-3, static-sta-private-key, static-key-0, static-key-1, static-key-2, management-protection-key, nv2-preshared-key, private-key, private-pre-shared-static-key-3, static-sta-private-key-Wir key, wpa-pre-shared-key, wpa2-pre-shared-key, mschapv2-password eless Interface#WEPproperties

management-protection-key, private- key, private-pre-shared-key-Wireless Interface#Properties

wpa-pre-shared-key, wpa2-pre-shared- key-Wireless Interface#WPAproperties

mschapv2-password-Wireless Interface#WPAEAPproperties

nv2-preshared-key-Wireless Interface#Generalinterfaceproperties

interface/w60g password W60G#Generalinterfaceproperties

zerotier identity ZeroTier#Parameters

certificate export-passphrase, passphrase, challenge-password, pin, key-passphrase, pin-used for card-reinstall and card- challenge-passphrase verify commands, no dedicated documentation page available.

export-passphrase-Certificates#Export Certificate

passphrase-Certificates#ImportCertific ate

challenge-password, key-passphrase, challenge-passphrase-Work in progress
