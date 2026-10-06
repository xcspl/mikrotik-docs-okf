---
type: Reference
title: "RouterOS license keys"
description: "MikroTik hardware routers that run RouterOS come preinstalled with a RouterOS license, if you have purchased a RouterOS based device, nothing must be done regarding the license."
timestamp: '2026-10-06'
status: active
tags: [routeros, mikrotik, networking]
resource: ~/Downloads/ROS-260526-1445-796.pdf
sources:
  - resource: https://manual.mikrotik.com/docs/introduction/
---

# RouterOS license keys

Overview System Requirements RouterOS license key levels CHR License Levels Prepaid Key How to Purchase a RouterOS license key How to Convert prepaid key to licence key for x86 Replacement Key Obtaining Licenses and Working With Them Where can I buy a RouterOS license key? If I have purchased my key elsewhere If I have a license and want to put it on another account? If I have lost a license on my device? Using the License Can I Format or Re-Flash the drive? How many computers can I use the License on? Can I temporary use the HDD for something else, other than RouterOS? Can I move the license to another HDD? Must I type the whole key into the router? Can I install another OS on my drive and then install RouterOS again later? I lost my RouterBOARD, can you give me the license to use on another system? Licenses Purchased from Resellers I am not using the software, can you terminate my license? Is this possible to upgrade or transfer my x86 license to a CHR license

## Overview

MikroTik hardware routers that run RouterOS come preinstalled with a RouterOS license, if you have purchased a RouterOS based device, nothing must be done regarding the license.

For X86 systems (i.e. PC devices), you need to obtain a license key. Each x86 system has a unique identifier called Software ID, which is used for licensing.

The license key is a block of symbols that needs to be copied from your mikrotik.com account, or from the email you received in, and then it can be pasted into the router. You can paste the key anywhere in the terminal, or by clicking "Paste key" in WinBox License menu. A reboot is required for the key to take effect.

RouterOS licensing scheme is based on Software ID / System ID where:

RouterBOARD Software ID is bound to storage media (HDD, NAND). x86 Software ID is bound to MBR CHR System ID is bound to MBR and UUID

Before the license purchase it is recommended to check if the Software ID does not change on reboot. (Software ID may change on defective HDD, on HDD where RAID controllers are used but not properly configured etc.)

Licensing information can be read from CLI system console:

[admin@RB1100] > /system license print software-id: "43NU-NLT9" nlevel: 6 features: [admin@RB1100] >

or from equivalent WinBox WebFig, menu.

## System Requirements

Package version: RouterOS v6.34 or newer Host CPU: x86-64 Architecture (64-bit) RAM: 512MB or more Disk: 128MB or more RouterOS version 6: The maximum supported hard drive size is 16GB RouterOS version 7: The maximum amount of RAM and disk space is limited by the Linux kernel 5.6.3 and depends on the specific hardware.

The minimum required RAM depends on interface count and CPU count. You can get an approximate number by using the following formula:

RouterOS v6 - RAM = 128 + [ 8 × (CPU_COUNT) × (INTERFACE_COUNT - 1)] RouterOS v7 - RAM = 512 + [ 8 × (CPU_COUNT) × (INTERFACE_COUNT - 1)]
