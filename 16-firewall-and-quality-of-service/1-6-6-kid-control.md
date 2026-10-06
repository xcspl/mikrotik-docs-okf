---
type: Reference
title: "Kid Control"
description: "\"Kid control\" is a parental control feature to limit internet connectivity for LAN devices."
timestamp: '2026-10-06'
status: active
tags: [routeros, mikrotik, networking]
resource: ~/Downloads/ROS-260526-1445-796.pdf
sources:
  - resource: https://manual.mikrotik.com/docs/introduction/
---

# Kid Control

Summary Property Description Devices Application example

## Summary

Sub-menu: /ip kid-control

"Kid control" is a parental control feature to limit internet connectivity for LAN devices.

## Property Description

In this menu, it is possible to create a profile for each Kid and restrict internet accessibility.

Property Description

name (string) Name of the Kid's profile

mon,tue,wed,thu,fri,sat,sun (time) Each day of the week. Time of day, when internet access should be allowed

disabled (yes | no) Whether restrictions are enabled

rate-limit (string) The maximum available data rate for flow

tur-mon,tur-tue,tur-wed,tur-thu,tur-fri,tur-sat,tur-sun (time) Time unlimited rate. Time of day, when internet access should be unlimited

Time unlimited rate parameters have higher priority than rate-limit parameter.

## Devices

Sub-menu: /ip kid-control device

This sub-menu contains information if there are multiple connected devices to the internet (phone, tablet, gaming console, tv etc.). The device is identified by the MAC address that is retrieved from the ARP table. The appropriate IP address is taken from there.

Property Description

name (string) Name of the device

mac-address (string) Devices mac-address

user (string) To which profile append the device

reset-counters ([id, name]) Reset bytes-up and bytes-down counters.

## Application example

With the following example we will restrict access for Peter's mobile phone:

Disabled internet access on Monday, Wednesday and Friday Allowed unlimited internet access on: Tuesday Thursday from 11:00-22:00 Sunday 15:00-22:00 Limited bandwidth to 3Mbps for Peter's mobile phone on Saturday from 18:30-21:00

[admin@MikroTik] > /ip kid-control add name=Peter mon="" tur-tue="00:00-24h" wed="" tur-thu="11:00-22:00" fri="" sat="18:30-22:00" tur-sun="15h-21h" rate-limit=3M [admin@MikroTik] > /ip kid-control device add name=Mobile-phone user=Peter mac-address=FF:FF:FF:ED:83:63

Internet access limitation is implemented by adding dynamic firewall filter rules or simple queue rules. Here are example firewall filter rules:

[admin@MikroTik] > /ip firewall filter print

1 D ;;; Mobile-phone, kid-control chain=forward action=reject src-address=192.168.88.254

2 D ;;; Mobile-phone, kid-control chain=forward action=reject dst-address=192.168.88.254

Dynamically created simple queue:

[admin@MikroTik] > /queue simple print Flags: X-disabled, I-invalid, D-dynamic

1 D ;;; Mobile-phone, kid-control name="queue1" target=192.168.88.254/32 parent=none packet-marks="" priority=8/8 queue=default-small /default-small limit-at=3M/3M max-limit=3M/3M burst-limit=0/0 burst-threshold=0/0 burst-time=0s/0s bucket-size=0.1/0.1

It is possible to monitor how much data is used by the specific device:

[admin@MikroTik] > /ip kid-control device print stats

Flags: X-disabled, D-dynamic, B-blocked, L-limited, I-inactive # NAME IDLE-TIME RATE-DOWN RATE-UP BYTES-DOWN BYTES-UP 1 BI Mobile- phone 30s 0bps 0bps 3438.1KiB 8.9KiB

It is also possible to pause Internet access for the created kids, it will restrict all access until resume is used, which will continue with configured settings:

[admin@MikroTik] > /ip kid-control pause Peter [admin@MikroTik] > /ip kid-control print Flags: X-disabled, P-paused, B-blocked, L-rate-limited # NAME SUN MON TUE WED THU FRI SAT 0 PB Peter 15h-21h 11h-22h 18:30h-22h

||UPnP Introduction Configuration General properties|The MikroTik RouterOS supports Universal Plug and Play architecture for transparent peer-to-peer network connectivity of personal computers and network-enabled intelligent devices or appliances. UPnP enables data communication between any two devices under the command of any control device on the network. Universal Plug and Play is completely independent of any particular physical medium. It supports networking with automatic discovery without any initial configuration, whereby a device can dynamically join a network. DHCP and DNS servers are optional and will be used if available on the network. UPnP implements a simple yet powerful NAT traversal solution, that enables the client to get full two-way peer-to-peer network support from behind the NAT. There are two interface types for UPnP: internal (the one local clients are connected to) and external (the one the Internet is connected to). A router may only have one active external interface with a 'public' IP address on it, and as many internal interfaces as needed, all with source-NATted 'internal' IP addresses. The protocol works by creating dynamic NAT entries. UPnP internal interface can create NAT mapping for any subnet, not just the subnet present on the internal interface, so caution must be used when setting internal interfaces. The UPnP protocol is used for many modern applications, like most DirectX games, as well as for various Windows Messenger features like remote assistance, application sharing, file transfer, voice, and video from behind a firewall.|
|---|---|---|
||/ip upnp||
||Property|Description|
|es))|allow-disable- external- interface (yes | no ; Default: y enabled (yes | no ; Default: no show-dummy- rule (yes | no ; Default: yes) UPnP Interfaces /ip upnp interfaces|whether or not the users are allowed to disable the router's external interface. This functionality (for users to be able to turn the router's external interface off without any authentication procedure) is required by the standard, but as it is sometimes not expected or unwanted in UPnP deployments which the standard was not designed for (it was designed mostly for home users to establish their own local networks), you can disable this behavior Enable UPnP service Enable a workaround for some broken implementations, which are handling the absence of UPnP rules incorrectly (for example, popping up error messages). This option will instruct the server to install a dummy (meaningless) UPnP rule that can be observed by the clients, which refuse to work correctly otherwise If you do not disable the allow-disable-external-interface, any user from the local network will be able (without any authentication procedures) to disable the router's external interface|
||Property|Description|

interface (string; Default: ) Interface name on which uPnP will be running

type (external | internal; Default: no) UPnP interface type:

external-the interface a global IP address is assigned to internal-router's local interface the clients are connected to

forced-external-ip (Ip; Default: ) Allow specifying what public IP to use if the external interface has more than one IP available.

In more complex setups with VLANs, where the VLAN interface is considered as the LAN interface, the VLAN interface itself should be specified as the internal interface for UPnP to work properly.

## Configuration Example

We have masquerading already enabled on our router:

[admin@MikroTik] ip upnp> /ip firewall src-nat print Flags: X-disabled, I-invalid, D-dynamic 0 chain=srcnat action=masquerade out-interface=ether1 [admin@MikroTik] ip upnp>

To enable the UPnP feature:

[admin@MikroTik] ip upnp> set enable=yes [admin@MikroTik] ip upnp> print enabled: yes allow-disable-external-interface: yes show-dummy-rule: yes [admin@MikroTik] ip upnp>

Now, all we have to do is to add interfaces:

[admin@MikroTik] ip upnp interfaces> add interface=ether1 type=external [admin@MikroTik] ip upnp interfaces> add interface=ether2 type=internal [admin@MikroTik] ip upnp interfaces> print Flags: X-disabled # INTERFACE TYPE 0 X ether1 external 1 X ether2 internal

[admin@MikroTik] ip upnp interfaces> enable 0,1

Now once the client from the internal interface side sends UPnP request, dynamic NAT rules will be created on the router, example rules could look something similar to these:

[admin@MikroTik] > ip firewall nat print Flags: X-disabled, I-invalid, D-dynamic

0 chain=srcnat action=masquerade out-interface=ether1

1 D ;;; upnp 192.168.88.10: ApplicationX chain=dstnat action=dst-nat to-addresses=192.168.88.10 to-ports=55000 protocol=tcp dst-address=10.0.0.1 in-interface=ether1 dst-port=55000

2 D ;;; upnp 192.168.88.10: ApplicationX chain=dstnat action=dst-nat to-addresses=192.168.88.10 to-ports=55000 protocol=udp dst-address=10.0.0.1 in-interface=ether1 dst-port=55000
