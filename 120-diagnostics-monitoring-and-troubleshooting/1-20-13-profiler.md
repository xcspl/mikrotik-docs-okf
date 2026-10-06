---
type: Reference
title: "Profiler"
description: "The profiler tool shows CPU usage for each process running in RouterOS. It helps to identify which process is using most of the CPU resources. Watch our video about this feature."
timestamp: '2026-05-26'
status: active
tags: [routeros, mikrotik, networking]
resource: ~/Downloads/ROS-260526-1445-796.pdf
sources:
  - resource: https://help.mikrotik.com/docs/spaces/ROS/pages/328059/RouterOS
---

# Profiler

Summary Classifiers

## Summary

The profiler tool shows CPU usage for each process running in RouterOS. It helps to identify which process is using most of the CPU resources. Watch our video about this feature.

[admin@MikroTik] > /tool/profile

On multi-core systems, the tool allows specifying per core CPU usage.

"CPU" parameter allows specifying integer number which represents a core or two of predefined values all and total:

total-this value sets to show the sum of all core usages; all-value sets to show CPU usages separately for every available core

In the following example we will take a look at both predefined values:

[admin@MikroTik] > /tool/profile cpu=all NAME CPU USAGE ethernet 1 0% kvm 0 0% kvm 1 4.5% management 0 0% management 1 0.5% idle 0 100% idle 1 93% profiling 0 0% profiling 1 2%

[admin@MikroTik] > /tool profile cpu=total NAME CPU USAGE ethernet all 0% console all 0% kvm all 2.7% management all 0% idle all 97.2% profiling all 0% bridging all 0%

## Classifiers

RouterOS processes are classified by type and the CPU usage for each type is displayed separately for ease of debugging.

Property Description

backup Backup service

bfd BFD service

bgp BGP service

bridging Bridging service

btest Bandwidth test.

certificate Certificate service

console

container

dhcp

disk

dns

dude

e-mail

encrypting

eoip

ethernet

fetcher

fileman

firewall

firewall-mgmt

flash

ftp

gps

graphing

gre

health

hotspot

idle

igmp-proxy

internet-detect

ip-pool

ipsec

Console

combined container usage

DHCP-Server and DHCP-Client services

storage-related services

DNS-related services

The Dude package services

e-mail tool

encrypting processes

EoIP

Ethernet-related properties like link speed, auto-negotiation, duplex mode, monitor a transceiver diagnostic information, etc.

Fetch tool

File manager

Firewall-related processes

Firewall Management: Filtering, NAT, Mangle

storage-related services

FTP Service

GPS Service

Graphing tool

GRE

system monitoring, workd health

Hotspot service

Free CPU resources

IGMP Proxy service

Detect Internet tool

IP Pool service

IPsec service: xfrm -  set of statistics showing numbers of packets dropped by the transformation code and why. drivers/crypto-drivers that provide access to the hardware cryptographic accelerators. ipsec-processes that relate to the Internet Key Exchange (IKE) protocols, Authentication Header (AH), Encapsulating Security Payload (ESP).

KVM virtual machine functionality

L7 matcher

LCD Interfaces system

Label Distribution Protocol (LDP)

Logging system

different subsystems: scheduler, networking, file management, etc.

MPLS-related features

Neighbour discovery service

kvm

l7-matcher

lcd

ldp

logging

management

mpls

neighbour- discovery

networking

ntp

ospf

ovpn

pim

profiling

queue-mgmt

queuing

radius

radv

remote-access

rip

routing

serial

sniffing

snmp

socks

spi

ssh

ssl

supout.rif

telnet

tftp

traffic-accounting

traffic-flow

unclassified

upnp

usb

user-manager

vrrp

web-proxy

winbox

wireguard

wireless

www

zerotier

common set of services included in the networking

NTP service

OSPF service

OVPN service

Protocol Independent Multicast

Profiler service

Queues: Simple queues, Queue tree, Queue types

Intermediate Queuing

RADIUS service

IPv6 radv daemon log messages service

accessing the device directly without logging into RouterOS

Routing Information Protocol

Routing-related services

serial console and terminal tool

packet Sniffer tool

SNMP

Socket Secure

storage-related services

SSH Server

SSL

supout.rif file generation

Telnet service

TFTP service

Traffic-Flow log system

Traffic-Flow system

processes or services that are not defined by this classifier

UPnP protocol

USB features

User Manager service

VRRP

Web Proxy

Winbox

Wireguard

common set of services using Wireless systems

Webfig HTTP service

ZeroTier
