---
type: Reference
title: "Resource"
description: "The general resource menu shows overall resource usage and router statistics like uptime, memory usage, disk usage, version, etc."
timestamp: '2026-10-06'
status: active
tags: [routeros, mikrotik, networking]
resource: ~/Downloads/ROS-260526-1445-796.pdf
sources:
  - resource: https://manual.mikrotik.com/docs/introduction/
---

# Resource

## Summary

General

/system resource

The general resource menu shows overall resource usage and router statistics like uptime, memory usage, disk usage, version, etc.

It also has several sub-menus for more detailed hardware statistics like CPU, IRQ, and Hardware.

[admin@MikroTik] > system/resource/print uptime: 29s version: 7.11.2 (stable) build-time: Aug/31/2023 13:55:47 factory-software: 7.6 free-memory: 94.2MiB total-memory: 224.0MiB cpu: ARM cpu-count: 2 cpu-frequency: 800MHz cpu-load: 2% free-hdd-space: 93.5MiB total-hdd-space: 128.5MiB write-sect-since-reboot: 85 write-sect-total: 222100 bad-blocks: 0% architecture-name: arm board-name: hAP ax lite LTE6 platform: MikroTik

Properties

All properties are read-only

Property Description

architecture-name (string) CPU architecture

bad-blocks (percent) Shows percentage of bad blocks on the NAND.

board-name (string) RouterBOARD model name

build-time (string) Installed RouterOS version build-time

cpu (string) CPU model that is on the board

cpu-count (integer) Number of CPUs present on the system. Each core is a separate CPU, Intel HT is also a separate CPU.

cpu-frequency (string) Current CPU frequency

cpu-load (percent) Percentage of used CPU resources. Combines all CPUs. Per-core CPU usage can be seen in CPU submenu

factory-software (string) Minimal RouterOS version

free-hdd-space (string) Free space on hard drive or NAND

free-memory (string) The unused amount of RAM

platform (string) Platform name

total-hdd-space (string) Size of the hard drive or NAND

total-memory (string) Amount of installed RAM

uptime (time) Time interval passed since boot-up

version (string) Installed RouterOS version number

write-sect-since-reboot (integer) A number of sector writes in HDD or NAND since the router was last time rebooted

write-sect-total (integer) A number of sector writes in total

CPU

/system resource cpu

This submenu shows per-cpu usage, as long as IRQ and Disk usage.

[admin@RB1100test] /system resource cpu> print

[admin@RB1100test] /system resource cpu>

Description

Identification number of CPU which usage is shown.

CPU usage in percents

IRQ usage in percents

Disk usage in percents

The menu shows all used IRQs on the router. It is possible to set up IRQ load balancing on multicore systems by assigning IRQ to a specific core. IRQ assignments are done by hardware and cannot be changed from RouterOS. For example, if all Ethernets are assigned to one IRQ, then you have to deal with hardware: upgrade motherboards BIOS, reassign IRQs manually in BIOS, if none of the above helps then change the hardware.

Properties

CPU LOAD IRQ DISK 0 5% 0% 0%

Properties

Read-only properties

Property

cpu (integer)

load (percent)

irq (percent)

disk (percent)

IRQ

/system resource irq

Description

Specifies which CPU is assigned to the IRQ.

auto - pick CPU based on a number of interrupts. Uses NAPI to optimize interrupts.

Description

Shows active CPU in multicore systems.

Property

cpu (auto | integer; Default: )

Read-only properties

Property

active-cpu (integer)

A number of interrupts. On ethernet interfaces interrupt=packet.

IRQ identification number

Process assigned to IRQ

Receive Packet Steering (RPS) is similar to Receive Side Scaling (RSS) in that it is used to direct packets to specific CPUs for processing. However, RPS is implemented at the software level, and helps to prevent the hardware queue of a single network interface card from becoming a bottleneck in network

RPS is useful when packets require additional processing that uses a relatively large amount of CPU time, such as PPP tunnel termination, VPLS, or firewall processing. The CPU resources spent by RPS on classifying and forwarding packets to another CPU are then outweighed by the additional processing required. Unfortunately, RPS cannot always replace several lines in Ethernet drivers, as forwarding packets to another CPU is expensive in

For network devices with multiple queues, there is typically no benefit to configuring both RPS and RSS, as RSS is configured to map a CPU to each receive queue by default. However, RPS may still be beneficial if there are fewer hardware queues than CPUs, depending on the traffic handled by the

Description

Disable RPS for selected entries

Edit properties of an existing entry

Enable RPS for selected entries

Reset properties to default values

Shows detected hardware devices connected via PCI, USB, or SCSI buses.

I-inactive Device is present but not active

count (integer)

irq (integer)

users (string)

RPS system/resource/irq/rps

traffic.

itself.

device.

Properties

Property

disable (number)

edit  (number)

enable (number)

reset (number)

Hardware

Flags:

/system/resource/hardware

Properties

Property

location (string)

parent (enum)

type (usb|pci|scsi|serial)

vendor (string)

name (string)

serial-number (string)

Description

Device location in system topology

Parent bus or controller

Bus type of the device

Device vendor name

Device name or model

Device serial number

|vendor-id (string)||Vendor identifier (VID)|
|---|---|---|
|device-id (string)||Device identifier (PID / Device ID)|
|speed (string)||Negotiated device speed|
|ports (number)||Number of ports provided by the device|
|usb-version (string)||Supported USB version|
|owner (string)||Subsystem or driver owning the device|
|device-path (string) Read-only properties||Device path from root bus to endpoint|
|Property|Description||
|category (string)|Device category||
|irq (number)|Assigned interrupt number||

### Device authorization

Controls authorization state of a hardware device. /system/resource/hardware/authorize

Properties

Property Description

allow (yes|no) Enable or disable USB device authorization

Global USB subsystem settings /system/resource/hardware/usb-settings

Properties

Property Description

authorization (yes|no) Enable or disable USB device authorization

numbers (number)

/system/resource/hardware/usb-power-reset

Properties

Property Description

duration (time) Power-off duration before re-enabling USB

bus (number) USB bus number

slot (number) USB port/slot number on the bus
