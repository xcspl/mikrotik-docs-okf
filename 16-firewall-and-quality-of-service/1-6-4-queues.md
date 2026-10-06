---
type: Reference
title: "Queues"
description: "A queue is a collection of data packets collectively waiting to be transmitted by a network device using a pre-defined structure methodology. Queuing works almost on the same methodology used at banks or supermarkets, wh."
timestamp: '2026-10-06'
status: active
tags: [routeros, mikrotik, networking]
resource: ~/Downloads/ROS-260526-1445-796.pdf
sources:
  - resource: https://manual.mikrotik.com/docs/introduction/
---

# Queues

Overview Rate limitation principles Simple Queue Flow Identifiers Other properties HTB Properties Statistics Configuration example Queue Tree Configuration example Queue Types Kinds FIFO RED SFQ PCQ CoDel FQ-Codel CAKE Interface Queue Queue load visualization in GUI

## Overview

A queue is a collection of data packets collectively waiting to be transmitted by a network device using a pre-defined structure methodology. Queuing works almost on the same methodology used at banks or supermarkets, where the customer is treated according to its arrival.

Queues are used to:

limit data rate for certain IP addresses, subnets, protocols, ports, etc.; limit peer-to-peer traffic; packet prioritization; configure traffic bursts for traffic acceleration; apply different time-based limits; share available traffic among users equally, or depending on the load of the channel

Queue implementation in MikroTik RouterOS is based on Hierarchical Token Bucket (HTB). HTB allows the creation of a hierarchical queue structure and determines relations between queues. These hierarchical structures can be attached at two different places, the Packet Flow diagram illustrates both input and postrouting chains.

There are two different ways how to configure queues in RouterOS:

/queue simple menu-designed to ease the configuration of simple, every day queuing tasks (such as single client upload/download limitation, p2p traffic limitation, etc.). /queue tree menu-for implementing advanced queuing tasks (such as global prioritization policy, and user group limitations). Requires marked packet flows from  /ip firewall mangle facility.

RouterOS provides a possibility to configure queue in 8 levels -  the first level is an interface queue from the "/queue interface" menu and the other 7 are lower-level queues that can be created in Queue Simple and/or Queue Tree.

### Rate limitation principles

Rate limiting is used to control the rate of traffic flow sent or received on a network interface. Traffic with rate that is less than or equal to the specified rate is sent, whereas traffic that exceeds the rate is dropped or delayed.

Rate limiting can be performed in two ways:

1. discard all packets that exceed rate limit – rate-limiting (dropper or shaper) (100% rate limiter when queue-size=0)

2. delay packets that exceed the specific rate limit in the queue and transmit them when it is possible – rate equalizing (scheduler) (100% rate equalizing when queue-size=unlimited)
The next figure explains the difference between rate limiting and rate equalizing:

As you can see in the first case all traffic exceeds a specific rate and is dropped. In another case, traffic exceeds a specific rate and is delayed in the queue and transmitted later when it is possible, but note that the packet can be delayed only until the queue is not full. If there is no more space in the queue buffer, packets are dropped.

For each queue we can define two rate limits:

CIR (Committed Information Rate) – (limit-at in RouterOS) worst-case scenario, the flow will get this amount of traffic rate regardless of other traffic flows. At any given time, the bandwidth should not fall below this committed rate. MIR (Maximum Information Rate) – (max-limit in RouterOS) best-case scenario, the maximum available data rate for flow, if there is free any part of the bandwidth.

## Simple Queue

/queue simple

A simple queue is a plain way how to limit traffic for a particular target. Also, you can use simple queues to build advanced QoS applications. They have useful integrated features:

peer-to-peer traffic queuing; applying queue rules on chosen time intervals; prioritization; using multiple packet marks from /ip firewall mangle traffic shaping (scheduling) of bidirectional traffic (one limit for the total of upload + download)

Simple queues have a <u>strict order</u> - each packet must go through every queue until it reaches one queue which conditions fit packet parameters or until the end of the queues list is reached. For example, In the case of 1000 queues, a packet for the last queue will need to proceed through 999 queues before it will reach the destination.

Simple queue target matches packets based on src and dst address. If src address matches target, then this is upload, if dst matches target, then this is download. However, if you have a connection where src and dst both match the target, then such packets will always be counted as download since both of them match dst (for each individual packet in both directions) which simply in RouterOS is the first thing compared to the target. Simple queue should be configured in a way that traffic can match only src or dst address, but not both of them at the same time.

Flow Identifiers

target (multiple choice: IP address/netmask or interface): Target is to be viewed from perspective of the target. If you want to limit your users' upload capability, set "target upload".

Each of these two properties can be used to determine which direction is target upload and which is download. Be careful to configure both of these options for the same queue-in case they will point to opposite directions queue will not work. If neither value of target nor of interface is specified, the queue will not be able to make the difference between upload and download and will limit all traffic twice.

Other properties

name (Text) : Unique queue identifier that can be used as parent option value for other queues both-limit both download and upload traffic upload-limit only traffic to the target download-limit only traffic from the target time (TIME-TIME,sun,mon,tue,wed,thu,fri,sat TIME-is local time, all day names are optional; default: not set) : allow to specify time when particular queue will be active. Router must have correct time settings. dst-address (IP address/netmask) : allows to select only specific stream (from target address to this destination address) for limitation explain what is target and what is dst and what is upload and what not packet-marks (Comma separated list of packet mark names) : allows to use marked packets from /ip firewall mangle. Take look at the RouterOS p acket flow diagram. It is necessary to mark packets before the simple queues (before global-in HTB queue) or else target's download limitation will not work. The only mangle chain before global-in is prerouting.

HTB Properties

parent (Name of parent simple queue, or none) : assigns this queue as a child queue for selected target {{{...}}}. Target queue can be HTB queue or any other previously created simple queue. In order for traffic to reach child queues, parent queues must capture all necessary traffic. priority (1..8) : Prioritize one child queue over other child queue. Does not work on parent queues (if queue has at least one child). One is the highest, eight is the lowest priority. Child queue with higher priority will have chance to reach its max-limit before child with lower priority. Priority have nothing to do with bursts. queue (SOMETHING/SOMETHING) : Choose the type of the upload/download queue. Queue types can be created in /queue type. limit-at (NUMBER/NUMBER) : normal upload/download data rate that is guaranteed to a target max-limit (NUMBER/NUMBER) : maximal upload/download data rate that is allowed for a target to reach to reach what burst-limit (NUMBER/NUMBER) : maximal upload/download data rate which can be reached while the burst is active burst-time (TIME/TIME) : period of time, in seconds, over which the average upload/download data rate is calculated. (This is NOT the time of actual burst) burst-threshold (NUMBER/NUMBER) : when average data rate is below this value-burst is allowed, as soon as average data rate reach this value-burst is denied. (basically this is burst on/off switch). For optimal burst behavior this value should above limit-at value and below max-limit value

And corresponding options for global-total HTB queue:

total-queue (SOMETHING/SOMETHING): corresponds to queue total-limit-at (NUMBER/NUMBER): corresponds to limit-at total-max-limit (NUMBER/NUMBER): corresponds to max-limit total-burst-limit (NUMBER/NUMBER): corresponds to burst-limit total-burst-time (TIME/TIME): corresponds to burst-time total-burst-threshold (NUMBER/NUMBER): corresponds to burst-threshold

Good practice suggests that:

Sum of children's limit-at values must be less or equal to max-limit of the parent.Every child's max-limit must be less than max-limit of the parent. This way you will leave some traffic for the other child queues, and they will be able to get traffic without fighting for it with other child queues.

Statistics

rate (read-only/read-only) : average queue passing data rate in bytes per second packet-rate (read-only/read-only) : average queue passing data rate in packets per second bytes (read-only/read-only) : number of bytes processed by this queue

packets (read-only/read-only) : number of packets processed by this queue queued-bytes (read-only/read-only) : number of bytes waiting in the queue queued-packets (read-only/read-only) : number of packets waiting in the queue dropped (read-only/read-only) : number of dropped packets borrows (read-only/read-only) : packets that passed queue over its "limit-at" value (and was unused and taken away from other queues) lends (read-only/read-only) : packets that passed queue below its "limit-at" value OR if queue is a parent-sum of all child borrowed packets pcq-queues (read-only/read-only) : number of PCQ substreams, if queue type is PCQ

And corresponding options for global-total HTB queue:

total-rate (read-only): corresponds to rate total-packet-rate (read-only): corresponds to packet-rate total-bytes (read-only): corresponds to bytes total-packets (read-only): corresponds to packets total-queued-bytes (read-only): corresponds to queued-bytes total-queued-packets (read-only): corresponds to queued-packets total-dropped (read-only): corresponds to dropped total-lends (read-only): corresponds to lends total-borrows (read-only): corresponds to borrows total-pcq-queues (read-only): corresponds to pcq-queues

## Configuration example

In the following example, we have one SOHO device with two connected units PC and Server.

We have a 15 Mbps connection available from ISP in this case. We want to be sure the server receives enough traffic, so we will configure a simple queue with a limit-at parameter to guarantee a server receives 5Mbps:

/queue simple add limit-at=5M/5M max-limit=15M/15M name=queue1 target=192.168.88.251/32

That is all. The server will get 5 Mbps of traffic rate regardless of other traffic flows. If you are using the default configuration, be sure the FastTrack rule is disabled for this particular traffic, otherwise, it will bypass Simple Queues and they will not work.

## Queue Tree

/queue tree

The queue tree creates only a one-directional queue in one of the HTBs. It is also the only way how to add a queue on a separate interface. This way it is possible to ease mangle configuration-you don't need separate marks for download and upload-only the upload will get to the Public interface and only the download will get to a Private interface. The main difference from Simple Queues is that the <u>Queue tree is not ordered</u> - all traffic passes it together.

### Configuration example

In the following example, we will mark all the packets coming from preconfigured in-interface-list=LAN and will limit the traffic with a queue tree based on these packet marks.

Let`s create a firewall address-list:

[admin@MikroTik] > /ip firewall address-list add address=www.youtube.com list=Youtube [admin@MikroTik] > ip firewall address-list print Flags: X-disabled, D-dynamic # LIST ADDRESS CREATION-TIME TIMEOUT 0 Youtube www.youtube. com oct/17/2019 14:47:11 1 D ;;; www.youtube.com Youtube

216.58.211.14 oct/17/2019 14:47:11 2 D ;;; www.youtube.com Youtube
216.58.207.238 oct/17/2019 14:47:11 3 D ;;; www.youtube.com Youtube
216.58.207.206 oct/17/2019 14:47:11 4 D ;;; www.youtube.com Youtube
172.217.21.174 oct/17/2019 14:47:11 5 D ;;; www.youtube.com Youtube
216.58.211.142 oct/17/2019 14:47:11 6 D ;;; www.youtube.com Youtube
172.217.22.174 oct/17/2019 14:47:21 7 D ;;; www.youtube.com Youtube
172.217.21.142 oct/17/2019 14:52:21
Mark packets with firewall mangle facility:

[admin@MikroTik] > /ip firewall mangle add action=mark-packet chain=forward dst-address-list=Youtube in-interface-list=LAN new-packet-mark=pmark- Youtube passthrough=yes

Configure the queue tree based on previously marked packets:

[admin@MikroTik] /queue tree add max-limit=5M name=Limiting-Youtube packet-mark=pmark-Youtube parent=global

Check Queue tree stats to be sure traffic is matched:

[admin@MikroTik] > queue tree print stats Flags: X-disabled, I-invalid 0 name="Limiting-Youtube" parent=global packet-mark=pmark-Youtube rate=0 packet-rate=0 queued-bytes=0 queued- packets=0 bytes=67887 packets=355 dropped=0

## Queue Types

/queue type

This sub-menu list by default created queue types and allows the addition of new user-specific ones.

By default, RouterOS creates the following pre-defined queue types:

[admin@MikroTik] > /queue type print Flags: * - default 0 * name="default" kind=pfifo pfifo-limit=50

1 * name="ethernet-default" kind=pfifo pfifo-limit=50

2 * name="wireless-default" kind=sfq sfq-perturb=5 sfq-allot=1514

3 * name="synchronous-default" kind=red red-limit=60 red-min-threshold=10 red-max-threshold=50 red-burst=20 red-avg-packet=1000

4 * name="hotspot-default" kind=sfq sfq-perturb=5 sfq-allot=1514

5 * name="pcq-upload-default" kind=pcq pcq-rate=0 pcq-limit=50KiB pcq-classifier=src-address pcq-total- limit=2000KiB pcq-burst-rate=0 pcq-burst-threshold=0 pcq-burst-time=10s pcq-src-address-mask=32 pcq-dst-address-mask=32 pcq-src-address6-mask=128 pcq-dst-address6-mask=128

6 * name="pcq-download-default" kind=pcq pcq-rate=0 pcq-limit=50KiB pcq-classifier=dst-address pcq-total- limit=2000KiB pcq-burst-rate=0 pcq-burst-threshold=0 pcq-burst-time=10s pcq-src-address-mask=32 pcq-dst-address-mask=32 pcq-src-address6-mask=128 pcq-dst-address6-mask=128

7 * name="only-hardware-queue" kind=none

8 * name="multi-queue-ethernet-default" kind=mq-pfifo mq-pfifo-limit=50

9 * name="default-small" kind=pfifo pfifo-limit=10

All MikroTik products have the default queue type "only-hardware-queue" with "kind=none". "only-hardware-queue" leaves the interface with only hardware transmit descriptor ring buffer which acts as a queue in itself. Usually, at least 100 packets can be queued for transmit in the transmit descriptor ring buffer. Transmit descriptor ring buffer size and the number of packets that can be queued in it varies for different types of ethernet MACs. Having no software queue is especially beneficial on SMP systems because it removes the requirement to synchronize access to it from different CPUs/cores which is resource-intensive. Having the possibility to set <u>"only-hardware-queue" requires support in an ethernet driver</u> so it is available only for some ethernet interfaces mostly found on RouterBOARDs.

A "multi-queue-ethernet-default" can be beneficial on SMP systems with ethernet interfaces that have support for multiple transmit queues and have a Linux driver support for multiple transmit queues. By having one software queue for each hardware queue there might be less time spent on synchronizing access to them.

Improvement from only-hardware-queue and multi-queue-ethernet-default is present only when there is no "/queue tree" entry with a particular interface as a parent.

Kinds

Queue kinds are packet processing algorithms. Kind describe which packet will be transmitted next in the line. RouterOS supports the following Queueing kinds:

FIFO (BFIFO, PFIFO, MQ PFIFO) RED SFQ PCQ

FIFO

These kinds are based on the FIFO algorithm (First-In-First-Out). The difference between PFIFO and BFIFO is that one is measured in packets and the other one in bytes. These queues use pfifo-limit and bfifo-limit parameters.

Every packet that cannot be enqueued (if the queue is full), is dropped. Large queue sizes can increase latency but utilize the channel better.

MQ-PFIFO is pfifo with support for multiple transmit queues. This queue is beneficial on SMP systems with ethernet interfaces that have support for multiple transmit queues and have a Linux driver support for multiple transmit queues (mostly on x86 platforms). This kind uses the mq-pfifo-limit parameter.

RED

Random Early Drop is a queuing mechanism that tries to avoid network congestion by controlling the <u>average queue size</u>. The average queue size is compared to two thresholds: a minimum (min ) and a maximum (max ) threshold. If the average queue size th th (avg ) is less than the minimum threshold, no q packets are dropped. When the average queue size is greater than the maximum threshold, all incoming packets are dropped. But if the average queue size is between the minimum and maximum thresholds packets are randomly dropped with probability P w d here probability is exact a function of the average queue size: P = P d max (avg – min )/ (max - min ). If the average queue grows, the probability of dr q th th th opping incoming packets grows too. Pmax-ratio, which can adjust the packet discarding probability abruptness, (the simplest case Pmax can be equal to one. The 8.2 diagram shows the packet drop probability in the RED algorithm.

SFQ

Stochastic Fairness Queuing (SFQ) is ensured by hashing and round-robin algorithms. SFQ is called "Stochastic" because it does not really allocate a queue for each flow, it has an algorithm that divides traffic over a limited number of queues (1024) using a hashing algorithm.

Traffic flow may be uniquely identified by 4 options (src-address, dst-address, src-port, and dst-port), so these parameters are used by the SFQ hashing algorithm to classify packets into one of 1024 possible sub-streams. Then round-robin algorithm will start to distribute available bandwidth to all sub- streams, on each round giving sfq-allot bytes of traffic. The whole SFQ queue can contain 128 packets and there are 1024 sub-streams available. The 8.3 diagram shows the SFQ operation:

PCQ

PCQ algorithm is very simple-at first, it uses selected classifiers to distinguish one sub-stream from another, then applies individual FIFO queue size and limitation on every sub-stream, then groups all sub-streams together and applies global queue size and limitation.

PCQ parameters:

pcq-classifier (dst-address | dst-port | src-address | src-port; default: "") : selection of sub-stream identifiers pcq-rate (number): maximal available data rate of each sub-steam pcq-limit (number): queue size of single sub-stream (in KiB) pcq-total-limit (number): maximum amount of queued data in all sub-streams (in KiB)

It is possible to assign a speed limitation to sub-streams with the pcq-rate option. If "pcq-rate=0" sub-streams will divide available traffic equally.

For example, instead of having 100 queues with 1000kbps limitation for download, we can have one PCQ queue with 100 sub-streams

PCQ has burst implementation identical to Simple Queues and Queue Tree:

pcq-burst-rate (number): maximal upload/download data rate which can be reached while the burst for substream is allowed pcq-burst-threshold (number): this is the value of burst on/off switch pcq-burst-time (time): a period of time (in seconds) over which the average data rate is calculated. (This is NOT the time of the actual burst)

PCQ also allows using different size IPv4 and IPv6 networks as sub-stream identifiers. Before it was locked to a single IP address. This is done mainly for IPv6 as customers from an ISP point of view will be represented by /64 network, but devices in customers network will be /128. PCQ can be used for both of these scenarios and more. PCQ parameters:

pcq-dst-address-mask (number): the size of the IPv4 network that will be used as a dst-address sub-stream identifier pcq-src-address-mask (number): the size of the IPv4 network that will be used as an src-address sub-stream identifier pcq-dst-address6-mask (number): the size of the IPV6 network that will be used as a dst-address sub-stream identifier pcq-src-address6-mask (number): the size of the IPV6 network that will be used as an src-address sub-stream identifier

The following queue kinds CoDel, FQ-Codel, and CAKE available since RouterOS version 7.1beta3.

CoDel

CoDel (Controlled-Delay Active Queue Management) algorithm uses the local minimum queue as a measure of the persistent queue, similarly, it uses a minimum delay parameter as a measure of the standing queue delay. Queue size is calculated using packet residence time in the queue.

Properties

Property Description

codel-ce-threshold (default: ) Marks packets above a configured threshold with ECN.

codel-ecn (default: no) An option is used to mark packets instead of dropping them.

codel-interval (default: 100ms) Interval should be set on the order of the worst-case RTT through the bottleneck giving endpoints sufficient time to react.

codel-limit (default: 1000) Queue limit, when the limit is reached, incoming packets are dropped.

codel-target (default: 5ms) Represents an acceptable minimum persistent queue delay.

FQ-Codel

CoDel-Fair Queuing (FQ) with Controlled Delay (CoDel) uses a model to classify incoming packets into different flows and is used randomly determined to provide a fair share of the bandwidth to all the flows using the queue. Each flow is managed using CoDel queuing discipline which internally uses a FIFO algorithm.

Properties

Property Description

fq-codel-ce-threshold (def Marks packets above a configured threshold with ECN. ault: )

fq-codel-ecn (default: yes) An option is used to mark packets instead of dropping them.

fq-codel-flows (default: 10 A number of flows into which the incoming packets are classified.

24) fq-codel-interval (default: 1 Interval should be set on the order of the worst-case RTT through the bottleneck giving endpoints sufficient time to react. 00ms) fq-codel-limit (default: 102 Queue limit, when the limit is reached, incoming packets are dropped.
40) fq-codel-memlimit A total number of bytes that can be queued in this FQ-CoDel instance. Will be enforced from the fq-codel-limit parameter. (default: 32.0MiB) fq-codel-quantum (default: A number of bytes used as 'deficit' in the fair queuing algorithm. Default (1514 bytes) corresponds to the Ethernet MTU
1514) plus the hardware header length of 14 bytes. fq-codel-target (default: 5 Represents an acceptable minimum persistent queue delay. ms) CAKE CAKE-Common Applications Kept Enhanced (CAKE) implemented as a queue discipline (qdisc) for the Linux kernel uses COBALT (AQM algorithm combining Codel and BLUE) and a variant of DRR++ for flow isolation. In other words, Cake’s fundamental design goal is user-friendliness. All settings are optional; the default settings are chosen to be practical in most common deployments. In most cases, the configuration requires only a bandwidth parameter to get useful results, Properties Property Description

cake-ack-filter (default: none )

cake-atm (default: ) Compensates for ATM cell framing, which is normally found on ADSL links.

cake-autorate-ingress (yes/no, Automatic capacity estimation based on traffic arriving at this qdisc. This is most likely to be useful with cellular links, default: ) which tend to change quality randomly.  The Bandwidth Limit parameter can be used in conjunction to specify an initial estimate. The shaper will periodically be set to a bandwidth slightly below the estimated rate.  This estimator cannot estimate the bandwidth of links downstream of itself.

cake-bandwidth (default: ) Sets the shaper bandwidth.

cake-diffserv (default: diffserv3) CAKE can divide traffic into "tins" based on the Diffserv field:

diffserv4 Provides a general-purpose Diffserv implementation with four tins: Bulk (CS1), 6.25% threshold, generally low priority. Best Effort (general), 100% threshold. Video (AF4x, AF3x, CS3, AF2x, CS2, TOS4, TOS1), 50% threshold. Voice (CS7, CS6, EF, VA, CS5, CS4), 25% threshold. diffserv3 (default) Provides a simple, general-purpose Diffserv implementation with three tins: Bulk (CS1),

6.25% threshold, generally low priority. Best Effort (general), 100% threshold. Voice (CS7, CS6, EF, VA, TOS4), 25% threshold, reduced Codel interval.
cake-flowmode (dsthost/dual- dsthost/dual-srchost/flowblind /flows/hosts/srchost/triple- isolate, default: triple-isolate)

cake-memlimit (default: )

cake-mpu ( -64 ... 256, default: )

cake-nat (default: no)

cake-overhead ( -64 ... 256, default: )

cake-overhead-scheme (default: )

cake-rtt (default: 100ms )

cake-rtt-scheme (datacentre /internet/interplanetary/lan /metro/none/oceanic/regional /satellite, default: )

flowblind-Disables flow isolation; all traffic passes through a single queue for each tin. srchost-Flows are defined only by source address. dsthost Flows are defined only by destination address. hosts-Flows are defined by source-destination host pairs. This is host isolation, rather than flow isolation. flows-Flows are defined by the entire 5-tuple of source address, a destination address, transport protocol, source port, and destination port. This is the type of flow isolation performed by SFQ and fq_codel. dual-srchost Flows are defined by the 5-tuple, and fairness is applied first over source addresses, then over individual flows. Good for use on egress traffic from a LAN to the internet, where it'll prevent any LAN host from monopolizing the uplink, regardless of the number of flows they use. dual-dsthost Flows are defined by the 5-tuple, and fairness is applied first over destination addresses, then over individual flows. Good for use on ingress traffic to a LAN from the internet, where it'll prevent any LAN host from monopolizing the downlink, regardless of the number of flows they use. triple-isolate-Flows are defined by the 5-tuple, and fairness is applied over source *and* destination addresses intelligently (ie. not merely by host-pairs), and also over individual flows. nat Instructs Cake to perform a NAT lookup before applying flow- isolation rules, to determine the true addresses and port numbers of the packet, to improve fairness between hosts "inside" the NAT. This has no practical effect in "flowblind" or "flows" modes, or if NAT is performed on a different host. nonat (default) The cake will not perform a NAT lookup. Flow isolation will be performed using the addresses and port numbers directly visible to the interface Cake is attached to.

Limit the memory consumed by Cake to LIMIT bytes. By default, the limit is calculated based on the bandwidth and RTT settings.

Rounds each packet (including overhead) up to a minimum length BYTES.

Instructs Cake to perform a NAT lookup before applying a flow-isolation rule.

Adds BYTES to the size of each packet. BYTES may be negative.

Manually specify an RTT. Default 100ms is suitable for most Internet traffic.

datacentre-For extremely high-performance 10GigE+ networks only. Equivalent to RTT 100us. lan-For pure Ethernet (not Wi-Fi) networks, at home or in the office. Don't use this when shaping for an Internet access link. Equivalent to RTT 1ms. metro-For traffic mostly within a single city. Equivalent to RTT 10ms. regional For traffic mostly within a European-sized country. Equivalent to RTT 30ms. internet (default) This is suitable for most Internet traffic. Equivalent to RTT 100ms. oceanic-For Internet traffic with generally above-average latency, such as that suffered by Australasian residents. Equivalent to RTT 300ms. satellite-For traffic via geostationary satellites. Equivalent to RTT 1000ms.

|cake-wash (default: no) Interface Queue|interplanetary-So named because Jupiter is about 1 light-hour from Earth. Use this to (almost) completely disable AQM actions. Equivalent to RTT 3600s. Apply the wash option to clear all extra DiffServ (but not ECN bits), after priority queuing has taken place.|
|---|---|
|/queue interface|Before sending data over an interface, it is processed by the queue. This sub-menu lists all available interfaces in RouterOS and allows to change queue type for a particular interface. The list is generated automatically.|
|# INTERFACE QUEUE ACTIVE-QUEUE|[admin@MikroTik] > queue interface print Columns: INTERFACE, QUEUE, ACTIVE-QUEUE 0 ether1 only-hardware-queue only-hardware-queue 1 ether2 only-hardware-queue only-hardware-queue 2 ether3 only-hardware-queue only-hardware-queue 3 ether4 only-hardware-queue only-hardware-queue 4 ether5 only-hardware-queue only-hardware-queue 5 ether6 only-hardware-queue only-hardware-queue 6 ether7 only-hardware-queue only-hardware-queue 7 ether8 only-hardware-queue only-hardware-queue 8 ether9 only-hardware-queue only-hardware-queue 9 ether10 only-hardware-queue only-hardware-queue 10 sfp-sfpplus1 only-hardware-queue only-hardware-queue 11 wlan1 wireless-default wireless-default 12 wlan2 wireless-default wireless-default|
|0% - 50% of max-limit used|Queue load visualization in GUI In Winbox and Webfig, a green, yellow, or red icon visualizes each Simple and Tree queue usage based on max-limit. 50%  - 75% of max-limit used 75% - 100% of max-limit used|

# HTB (Hierarchical Token Bucket)

Introduction Token Bucket algorithm (Red part of the diagram) Packet queue (Blue part of the diagram) Token rate selection (Black part of the diagram) The Diagram Bucket Size in action Default Queue Bucket Large Queue Bucket Large Child Queue Bucket, Small Parent Queue Bucket Configuration Dual Limitation Priority Examples Structure Example 1: Usual case Result of Example 1 Example 2: Usual case with max-limit Result of Example 2 Example 3: Inner queue limit-at Result of Example 3 Example 4: Leaf queue limit-at Result of Example 4

## Introduction

HTB (Hierarchical Token Bucket) is a classful queuing discipline that is useful for rate limiting and burst handling. This article will focus on those HTB aspects exclusively in RouterOS, as we use a modified version to deliver features like Simple Queue and Queue Tree.

## Token Bucket algorithm (Red part of the diagram)

The Token Bucket algorithm is based on an analogy to a bucket where tokens, represented in bytes, are added at a specific rate. The bucket itself has a specified capacity.

If the bucket fills to capacity, newly arriving tokens are dropped.

Bucket capacity = bucket-size * max-limit

bucket size (0..10, Default:0.1)

Before allowing any packet to pass through the queue, the queue bucket is inspected to see if it already contains sufficient tokens at that moment.

If yes, the appropriate number of tokens are removed ("cashed in") and the packet is permitted to pass through the queue.

If not, the packets stay at the start of the packet waiting queue until the appropriate amount of tokens is available.

In the case of a multi-level queue structure, tokens used in a child queue are also 'charged' to their parent queues. In other words-child queues 'borrow' tokens from their parent queues.

Packet queue (Blue part of the diagram)

The size of this packet queue, the sequence, how packets are added to this queue, and when packets are discarded is determined by:

queue-type-Queue queue-size-Queue Size

Token rate selection (Black part of the diagram)

The maximal token rate at any given time is equal to the highest activity of these values:

limit-at (NUMBER/NUMBER): guaranteed upload/download data rate to a target max-limit (NUMBER/NUMBER): maximal upload/download data rate that is allowed for a target burst-limit (NUMBER/NUMBER): maximal upload/download data rate that is allowed for a target while the 'burst' is active

burst-limit is active only when 'burst' is in the allowed state-more info here: Queue Burst

In a case where limit-at is the highest value, extra tokens need to be issued to compensate for all missing tokens that were not borrowed from its parent queue.

### The Diagram

### Bucket Size in action

Let's have a simple setup where all traffic from and to one IP address is marked with a packet-mark:

/ip firewall mangle add chain=forward action=mark-connection connection-mark=no-mark src-address=192.168.88.101 new-connection- mark=pc1_conn add chain=forward action=mark-connection connection-mark=no-mark dst-address=192.168.88.101 new-connection- mark=pc1_conn add chain=forward action=mark-packet connection-mark=pc1_conn new-packet-mark=pc1_traffic

Default Queue Bucket

/queue tree add name=download parent=Local packet-mark=PC1-traffic max-limit=10M add name=upload parent=Public packet-mark=PC1-traffic max-limit=10M

In this case bucket-size=0.1, so bucket-capacity= 0.1 x 10M = 1M

If the bucket is full (that is, the client was not using the full capacity of the queue for some time), the next 1Mb of traffic can pass through the queue at an unrestricted speed.

Large Queue Bucket

/queue tree add name=download parent=Local packet-mark=PC1-traffic max-limit=10M bucket-size=10 add name=upload parent=Public packet-mark=PC1-traffic max-limit=10M bucket-size=10

Let's try to apply the same logic to a situation when bucket size is at its maximal value:

In this case bucket-size=10, so bucket-capacity= 10 x 10M = 100M

If the bucket is full (that is, the client was not using the full capacity of the queue for some time), the next 100Mb of traffic can pass through the queue at an unrestricted speed.

So you can have:

20Mbps transfer speed for 10s 60Mbps transfer burst for 2s 1Gbps transfer burst for approximately 100ms

You can therefore see that the bucket permits a type of 'burstiness' of the traffic that passes through the queue. The behavior is similar to the normal burst feature but lacks the upper limit of the burst. This setback can be avoided if we utilize bucket size in the queue structure:

Large Child Queue Bucket, Small Parent Queue Bucket

/queue tree add name=download_parent parent=Local max-limit=20M add name=download parent=download_parent packet-mark=PC1-traffic max-limit=10M bucket-size=10 add name=upload_parent parent=Public max-limit=20M add name=upload parent=upload_parent packet-mark=PC1-traffic max-limit=10M bucket-size=10

In this case:

parent queue bucket-size=0.1, bucket-capacity= 0.1 x 20M = 2M child queue bucket-size=10, bucket-capacity= 10 x 10M = 100M

The parent will run out of tokens much faster than the child queue and as its child queue always borrows tokens from the parent queue the whole system is restricted to token-rate of the parent queue-in this case to max-limit=20M. This rate will be sustained until the child queue runs out of tokens and will be restricted to its token rate of 10Mbps.

In this way, we can have a burst at 20Mbps for up to 10 seconds.

## Configuration

We have to follow three basic steps to create HTB:

Match and mark traffic – classify traffic for further use. Consists of one or more matching parameters to select packets for the specific class; Create rules (policy) to mark traffic – put specific traffic classes into specific queues and define the actions that are taken for each class; Attach a policy for specific interface(-s) – append policy for all interfaces (global-in, global-out, or global-total), for a specific interface, or for a specific parent queue;

HTB allows to create of a hierarchical queue structure and determines relations between queues, like "parent-child" or "child-child".

As soon as the queue has at least one child it becomes an inner queue, all queues without children-are leaf queues. Leaf queues make actual traffic consumption, Inner queues are responsible only for traffic distribution. All leaf queues are treated on an equal basis.

In RouterOS, it is necessary to specify parent option to assign a queue as a child to another queue. the

### Dual Limitation

Each queue in HTB has two rate limits:

CIR (Committed Information Rate) – (limit-at in RouterOS) worst case scenario, the flow will get this amount of traffic no matter what (assuming we can actually send so much data); MIR (Maximal Information Rate) – (max-limit in RouterOS) best case scenario, a rate that flow can get up to if their queue's parent has spare bandwidth;

In other words, at first limit-at (CIR) of all queues will be satisfied, only then child queues will try to borrow the necessary data rate from their parents in order to reach their max-limit (MIR).

CIR will be assigned to the corresponding queue no matter what. (even if max-limit of the parent is exceeded)

That is why, to ensure optimal (as designed) usage of the dual limitation feature, we suggest sticking to these rules:

The Sum of committed rates of all children must be less or equal to the amount of traffic that is available to parents;

CIR(parent)* ≥ CIR(child1) +...+ CIR(childN)*in case if parent is main parent CIR(parent)=MIR(parent)

The maximal rate of any child must be less or equal to the maximal rate of the parent

MIR (parent) ≥ MIR(child1) & MIR (parent) ≥ MIR(child2) & ... & MIR (parent) ≥ MIR(childN)

Queue colors in Winbox:

0% - 50% available traffic used-green 51% - 75% available traffic used-yellow 76% - 100% available traffic used-red

Priority

We already know that limit-at (CIR) to all queues will be given out no matter what.

Priority is responsible for the distribution of remaining parent queues traffic to child queues so that they are able to reach max-limit

The queue with higher priority will reach its max-limit before the queue with lower priority. 8 is the lowest priority, and 1 is the highest.

Make a note that priority only works:

for leaf queues-priority in the inner queue has no meaning. if max-limit is specified (not 0)

Examples

In this section, we will analyze HTB in action. To do that we will take one HTB structure and will try to cover all the possible situations and features, by changing the amount of incoming traffic that HTB has to recycle. and changing some options.

Structure

Our HTB structure will consist of 5 queues:

Queue01 inner queue with two children-Queue02 and Queue03 Queue02 inner queue with two children-Queue04 and Queue05 Queue03 leaf queue Queue04 leaf queue Queue05 leaf queue

Queue03, Queue04, and Queue05 are clients who require 10Mbps all the time Outgoing interface is able to handle 10Mbps of traffic.

Example 1: Usual case

Queue01 limit-at=0Mbps max-limit=10Mbps Queue02 limit-at=4Mbps max-limit=10Mbps Queue03 limit-at=6Mbps max-limit=10Mbps priority=1 Queue04 limit-at=2Mbps max-limit=10Mbps priority=3 Queue05 limit-at=2Mbps max-limit=10Mbps priority=5

Result of Example 1

Queue03 will receive 6Mbps Queue04 will receive 2Mbps Queue05 will receive 2Mbps Clarification: HTB was built in a way, that, by satisfying all limit-ats, the main queue no longer has throughput to distribute.

Example 2: Usual case with max-limit

Queue01 limit-at=0Mbps max-limit=10Mbps Queue02 limit-at=4Mbps max-limit=10Mbps Queue03 limit-at=2Mbps max-limit=10Mbps priority=3 Queue04 limit-at=2Mbps max-limit=10Mbps priority=1 Queue05 limit-at=2Mbps max-limit=10Mbps priority=5

Result of Example 2

Queue03 will receive 2Mbps Queue04 will receive 6Mbps Queue05 will receive 2Mbps Clarification: After satisfying all limit-ats HTB will give throughput to the queue with the highest priority.

Example 3: Inner queue limit-at

Queue01 limit-at=0Mbps max-limit=10Mbps Queue02 limit-at=8Mbps max-limit=10Mbps Queue03 limit-at=2Mbps max-limit=10Mbps priority=1 Queue04 limit-at=2Mbps max-limit=10Mbps priority=3 Queue05 limit-at=2Mbps max-limit=10Mbps priority=5

Result of Example 3

Queue03 will receive 2Mbps Queue04 will receive 6Mbps Queue05 will receive 2Mbps Clarification: After satisfying all limit-ats HTB will give throughput to the queue with the highest priority. But in this case, inner queue Queue02 had l imit-at specified, by doing so, it reserved 8Mbps of throughput for queues Queue04 and Queue05. Of these two Queue04 has the highest priority, which is why it gets additional throughput.

Example 4: Leaf queue limit-at

Queue01 limit-at=0Mbps max-limit=10Mbps Queue02 limit-at=4Mbps max-limit=10Mbps Queue03 limit-at=6Mbps max-limit=10Mbps priority=1 Queue04 limit-at=2Mbps max-limit=10Mbps priority=3 Queue05 limit-at=12Mbps max-limit=15Mbps priority=5

Result of Example 4

Queue03 will receive ~3Mbps Queue04 will receive ~1Mbps Queue05 will receive ~6Mbps Clarification: Only by satisfying all limit-ats HTB was forced to allocate 20Mbps - 6Mbps to Queue03, 2Mbps to Queue04, and 12Mbps to Queue05, but our output interface is able to handle 10Mbps. As the output interface queue is usually FIFO throughput allocation will keep the ratio 6:2:12 or 3:1:6
