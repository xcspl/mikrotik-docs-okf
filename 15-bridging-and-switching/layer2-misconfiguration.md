---
type: Reference
title: "Layer2 misconfiguration"
description: "There are certain configurations that are known to have major flaws by design and should be avoided by all means possible. Misconfigured Layer2 can sometimes cause hard to detect network errors, random performance drops,."
timestamp: '2026-10-06'
status: active
tags: [routeros, mikrotik, networking]
resource: ~/Downloads/ROS-260526-1445-796.pdf
sources:
  - resource: https://manual.mikrotik.com/docs/introduction/
---

# Layer2 misconfiguration

Introduction Bridges on a single switch chip Configuration Problem Symptoms Solution Packet flow with hardware offloading and MAC learning Configuration Problem Symptoms Solution LAG interfaces and load balancing Configuration Problem Symptoms Solution VLAN interface on a slave interface Configuration Problem Symptoms Solution VLAN on a bridge in a bridge Configuration Problem Symptoms Solution VLAN in a bridge with a physical interface Configuration Problem Symptoms Solution Bridged VLAN on physical interfaces Configuration Problem Symptoms Solution Bridged VLAN Configuration Symptoms Solution Bridge VLAN filtering without hardware offloading Configuration Problem Symptoms Solution VLAN filtering with multiple switch chips Configuration Problem Symptoms Solution VLAN filtering with simplified bridge VLAN table Configuration Problem Symptoms Solution MTU on the master interface Configuration Problem Symptoms Solution MTU inconsistency

Configuration Problem Symptoms Solution Bridge and reserved MAC addresses Configuration Problem Symptoms Solution Bonding between Wireless links Configuration Problem Symptoms Solution Bandwidth testing Problem Symptoms Solution Bridge split-horizon usage Configuration Problem Symptoms Solution Unsupported SFP modules Problem Symptoms Solution

## <u>Introduction</u>

There are certain configurations that are known to have major flaws by design and should be avoided by all means possible. Misconfigured Layer2 can sometimes cause hard to detect network errors, random performance drops, certain segments of a network to be unreachable, certain networking services to be malfunctioning, or a complete network failure. This page will contain some common and not so very common configurations that will cause issues in your network.

## <u>Bridges on a single switch chip</u>

Consider the following scenario, you have a device with a built-in switch chip and you need to isolate certain ports from each other, for this reason, you have created multiple bridges and enabled hardware offloading on them. Since each bridge is located on a different Layer2 domain, then Layer2 frames will not be forwarded between these bridges, as a result, ports in each bridge are isolated from other ports on a different bridge.

Configuration

/interface bridge add name=bridge1 add name=bridge2 /interface bridge port add bridge=bridge1 interface=ether1 add bridge=bridge1 interface=ether2 add bridge=bridge2 interface=ether3 add bridge=bridge2 interface=ether4

## Problem

After a simple performance test, you might notice that one bridge is capable of forwarding traffic at wire speed while the second, third, etc. bridge is not able to forward as much data as the first bridge. Another symptom might be that there exists a huge latency for packets that need to be routed. After a quick inspection, you might notice that the CPU is always at full load, this is because hardware offloading is not available on all bridges, but is available only on one bridge. By checking the hardware offloading status you will notice that only one bridge has it active:

[admin@MikroTik] > /interface bridge port print Flags: X-disabled, I-inactive, D-dynamic, H-hw-offload # INTERFACE BRIDGE HW 0 H ether1 bridge1 yes 1 H ether2 bridge1 yes 2 ether3 bridge2 yes 3 ether4 bridge2 yes

The reason why only one bridge has the hardware offloading flag available is that the device does not support port isolation. If port isolation is not supported, then only one bridge will be able to offload the traffic to the switch chip.

Symptoms

Below is a list of possible symptoms that might be a result of this kind of misconfiguration:

Missing "H" flag to bridge ports Low throughput High CPU usage

Solution

Not all device devices support port isolation, currently only CRS1xx/CRS2xx series devices support it and only 7 isolated and hardware offloaded bridges are supported at the same time, other devices will have to use the CPU to forward the packets on other bridges. This is usually a hardware limitation and a different device might be required. Bridge split-horizon parameter is a software feature that disables hardware offloading and when using bridge filter rules you need to enable forward all packets to the CPU, which requires the hardware offloading to be disabled. You can control which bridge will be hardware offloaded with the hw=yes flag and by setting hw=no to other bridges, for example:

/interface bridge port set [find where bridge=bridge1] hw=no /interface bridge port set [find where bridge=bridge2] hw=yes

Sometimes it is possible to restructure a network topology to use VLANs, which is the proper way to isolate Layer2 networks.

## <u>Packet flow with hardware offloading and MAC learning</u>

Consider the following scenario, you set up a bridge and have enabled hardware offloading in order to maximize the throughput for your device, as a result, your device is working as a switch, but you want to use Sniffer or Torch tools for debugging purposes, or maybe you want to implement packet logging.

Configuration

/interface bridge add name=bridge1 /interface bridge port add bridge=bridge1 hw=yes interface=ether1 learn=yes add bridge=bridge1 hw=yes interface=ether2 learn=yes

Problem

When running Sniffer or Torch tools to capture packets you might notice that barely any packets are visible, only some unicast packets, but mostly broadcast/multicast packets are captured, while the interfaces report that much larger traffic is flowing through certain interfaces than the traffic that was captured. If you add two or more Ethernet interfaces to a bridge and enable Hardware Offloading, then the switch chip will be used to forward packets between ports. To understand why only some packets are captured, we must first examine how the switch chip is interconnected with the CPU, in this example, we can use a block diagram from a generic 5-Port Ethernet router:

For this device, each Ethernet port is connected to the switch chip and the switch chip is connected to the CPU using the CPU port (sometimes called the s witch-cpu port). For packets to be visible in Sniffer or Torch tools, the packet must be sent from an Ethernet p ort to the CPU port, this means that the packet must be destined to the CPU port (destination MAC address of the packet matches the bridge's MAC address) or the packet's MAC address has not be learnt (packet is flooded to all ports), this behavior is because of MAC learning·

The switch chip keeps a list of MAC addresses and ports called the Host table· Whenever a packet needs to be forwarded, the switch chip checks the packet's destination MAC address against the hosts table to find which port should it use to forward the packet. If the switch chip cannot find the destination MAC address, then the packet is flooded to all ports (including the CPU port). In situations where a packet is supposed to be forwarded from, for example, ether1 to ether2 and the MAC address for the device behind ether2 is in the host table, then the packet is never sent to the CPU and therefore will not be visible to Sniffer or Torch tool.

Symptoms

Below is a list of possible symptoms that might be a result of this kind of misconfiguration:

Packets not visible by Sniffer or Torch tool Filter rules not working

Solution

Packets with a destination MAC address that has been learned will not be sent to the CPU since the packets are not being flooded to all ports. If you do need to send certain packets to the CPU for a packet analyzer or a firewall, then it is possible to copy or redirect the packet to the CPU by using ACL rules. Below is an example of how to send a copy of packets that are meant for 4C:5E:0C:4D:12:4B:

/interface ethernet switch rule add copy-to-cpu=yes dst-mac-address=4C:5E:0C:4D:12:4B/FF:FF:FF:FF:FF:FF ports=ether1 switch=switch1

If the packet is sent to the CPU, then the packet must be processed by the CPU, this increases the CPU load.
