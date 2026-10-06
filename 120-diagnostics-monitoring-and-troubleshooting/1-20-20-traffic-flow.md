---
type: Reference
title: "Traffic Flow"
description: "Traffic Flow can process only that traffic which is processed by the router CPU, thus HW offloaded traffic will not be seen in Traffic Flow flows (for example, HW offloaded bridged traffic)."
timestamp: '2026-05-26'
status: active
tags: [routeros, mikrotik, networking]
resource: ~/Downloads/ROS-260526-1445-796.pdf
sources:
  - resource: https://manual.mikrotik.com/docs/introduction/
---

# Traffic Flow

Introduction General Targets IPFIX Notes Examples See more

## Introduction

MikroTik Traffic-Flow is a system that provides statistical information about packets that pass through the router. Besides network monitoring and accounting, system administrators can identify various problems that may occur in the network. With help of Traffic-Flow, it is possible to analyze and optimize the overall network performance. As Traffic-Flow is compatible with Cisco NetFlow, it can be used with various utilities which are designed for Cisco's NetFlow.

Traffic Flow can process only that traffic which is processed by the router CPU, thus HW offloaded traffic will not be seen in Traffic Flow flows (for example, HW offloaded bridged traffic).

Traffic-Flow supports the following NetFlow formats:

version 1 - This is the original format used by NetFlow. It provides basic information about IP packets flowing through a router but lacks support for advanced features such as different types of protocols and Type of Service (ToS). version 5 - An enhancement over Version 1, this format supports additional features such as Type of Service (ToS), TCP flags, and autonomous system numbers. In addition to version 1, version 5 can include BGP AS and flow sequence number information. Currently, RouterOS does not include BGP AS numbers. version 9 - This version introduces a template-based export format, which allows for extensibility and support for new record types beyond what previous versions could handle. It can export data based on a defined template and is capable of exporting both IPv4 and IPv6 flow information. IPFIX-Standardized by the IETF, this protocol is based on NetFlow Version 9. It expands the capabilities further, allowing for more customizable and flexible flow records. IPFIX supports new technologies that were not addressed by NetFlow, like multicast.

## General

Sub-menu: /ip traffic-flow

This section lists the configuration properties of Traffic-Flow.

Property Description

interfaces (string | all; Names of those interfaces will be used to gather statistics for traffic-flow. To specify more than one interface, separate Default: all) them with a comma.

cache-entries (128k | 16k | Number of flows which can be in router's memory simultaneously. 1k | 256k | 2k | ...; Default: 4k)

active-flow-timeout (time; Maximum life-time of a flow. Default: 30m)

inactive-flow-timeout (time; How long to keep the flow active, if it is idle. If a connection does not see any packet within this timeout, then traffic-flow Default: 15s) will send a packet out as a new flow. If this timeout is too small it can create a significant amount of flows and overflow the buffer.

packet-sampling (no | yes; Enable or disable packet sampling feature. Default: no)

sampling-interval (integer; The number of packets that are consecutively sampled. Default: 0)

sampling-space (integer; The number of packets that are consecutively omitted. Default: 0)

|info|Packet sampling is available in RouterOS v7. In the following example:|/ip/traffic-flow/set packet-sampling=yes sampling-interval=2222 sampling-space=1111|
|---|---|---|
|Targets|Sub-menu: /ip traffic-flow target|2222 packet consecutive packets will be sampled and then 1111 will be omitted. Then the sampling cycle repeats in such a manner. With Traffic-Flow targets we specify those hosts which will gather the Traffic-Flow information from the router.|
|Property||Description|
|IPFIX|src-address (IP; Default:) dst- address (IP; Default:) Port (Port; Default:2055) v9-template-refresh (integer; Default: 20) v9-template-timeout (time; Default:) version (1 | 5 | 9 | IPFIX; Default:) Sub-menu: /ip traffic-flow ipfix Allows to customize flow records|IP address used as source when sending Traffic-Flow statistics IP address of the host which receives Traffic-Flow statistic packets from the router. Port (UDP) of the host which receives Traffic-Flow statistic packets from the router. Number of packets after which the template is sent to the receiving host (only for NetFlow version 9 and IPFIX) After how long to send the template, if it has not been sent. (only for NetFlow version 9 and IPFIX) Which version format of NetFlow to use|
|Property|Description||
|bytes ip-total-lenght src-address dst-address ipv6-flow-label src-address-mask dst-address-mask is-multicast src-mac-address dst-mac-address last-forwarded|Source MAC address.|Total number of bytes processed in the flow. Length of the IP packet in bytes. The source IP address of the flow. The destination IP address of the flow. Label field from an IPv6 header, used to classify flows. Network mask for the source address, useful in summarizing data. Network mask for the destination address. Indicates whether the flow is a multicast flow. Destination MAC address. Timestamp of the last packet forwarded in a flow.|

src-port

dst-port

nat-dst-address

sys-init-time

first-forwarded

nat-dst-port

tcp-ack-num

gateway

nat-events

tcp-flags

icmp-code

nat-src-address

icmp-type

nat-src-port

tcp-seq-num

tcp-window-size

igmp-type

out-interface

in-interface

packets

ip-header-length

protocol

tos

ttl

udp-length

Source port number.

Destination port number.

Translated destination IP address by NAT.

System initialization time, can be used for timing analysis.

Timestamp of the first packet forwarded in a flow.

Translated destination port number by NAT.

Acknowledgment number in a TCP connection.

IP address of the gateway through which the flow was routed.

Events related to Network Address Translation for the flow.

Flags from the TCP header (e.g., SYN, ACK).

ICMP code for error messaging and operational information.

Translated source IP address by NAT.

Type of ICMP message, important for diagnostic messages.

Translated source port number by NAT.

Sequence number in a TCP connection.

Window size in a TCP connection, indicating the scale of received data buffering.

Type of Internet Group Management Protocol operation.

Interface through which packets of the flow are sent out.

Interface through which packets of the flow are received.

Number of packets processed in the flow.

Length of the IP header.

Protocol number (e.g., TCP, UDP, ICMP).

Type of Service field in the IP header, indicating priority and handling of the packet.

Time To Live for the packet, decremented by each router to prevent infinite loops.

Length of the UDP payload.

## Notes

## Examples

By looking at the packet flow diagram you can see that traffic flow is at the end of the input, forward, and output chain stack. It means that traffic flow will count only traffic that reaches one of those chains.

For example, you set up a mirror port on a switch, connect the mirror port to a router, and set traffic flow to count mirrored packets. Unfortunately, such a setup will not work, because mirrored packets are dropped before they reach the input chain.

Other interfaces will appear in the report if traffic is passing through them and the monitoring interface.

This example shows how to configure Traffic-Flow on a router

Enable Traffic-Flow on the router:

[admin@MikroTik] ip traffic-flow> set enabled=yes [admin@MikroTik] ip traffic-flow> print enabled: yes interfaces: all cache-entries: 1k active-flow-timeout: 30m inactive-flow-timeout: 15s [admin@MikroTik] ip traffic-flow>

Specify the IP address and port of the host, which will receive Traffic-Flow packets:

[admin@MikroTik] ip traffic-flow target> add dst-address=192.168.0.2 port=2055 version=9 [admin@MikroTik] ip traffic-flow target> print Flags: X-disabled # SRC-ADDRESS DST-ADDRESS PORT VERSION 0 0.0.0.0 192.168.0.2 2055 9 [admin@MikroTik] ip traffic-flow target>

Now the router starts to send packets with Traffic-Flow information.

Note

To use ntop-ng with MikroTik you need to use Nprobe, which is paid software.

### See more

NetFlow Fundamentals Traffic flow with Ntop on MikroTik
