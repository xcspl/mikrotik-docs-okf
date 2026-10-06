---
type: Reference
title: "RouterOS license key levels"
description: "After installation RouterOS runs in trial mode. You have 24 hours to register for Level 1 (Free demo) or purchase a Level 4,5 or 6 license and paste a valid key."
timestamp: '2026-05-26'
status: active
tags: [routeros, mikrotik, networking]
resource: ~/Downloads/ROS-260526-1445-796.pdf
sources:
  - resource: https://manual.mikrotik.com/docs/introduction/
---

# RouterOS license key levels

After installation RouterOS runs in trial mode. You have 24 hours to register for Level 1 (Free demo) or purchase a Level 4,5 or 6 license and paste a valid key.

[admin@MikroTik] /system license> print software-id: TRPC-YYR2 expires-in: 23h48m24s

Level 3 is a wireless station (client or CPE) only license. For x86 PCs, Level3 is not available for purchase individually.

Level 2 was a transitional license from old legacy (pre 2.8) license format. These licenses are not available any more, if you have this kind of license, it will work, but to upgrade it-you will have to purchase a new license.

The difference between license levels is shown in the table below:

|Level number||0 (Trial mode)|1 (Free Demo)|3 (WISP CPE)|4 (WISP)|5 (WISP)|6 (Controller)|
|---|---|---|---|---|---|---|---|
|Price||no key|registration required|not for sale|$45|$95|$250|
|Wireless4 AP mode (PtMP)||24h trial|-|no|yes|yes|yes|
|Wireless6 AP mode||-|-|yes|yes|yes|yes|
|PPPoE tunnels||24h trial|1|200|200|500|unlimited|
|PPTP tunnels||24h trial|1|200|200|500|unlimited|
|L2TP tunnels||24h trial|1|200|200|500|unlimited|
|OVPN tunnels||24h trial|1|200|200|unlimited|unlimited|
|EoIP tunnels||24h trial|1|unlimited|unlimited|unlimited|unlimited|
|VLAN interfaces||24h trial|1|unlimited|unlimited|unlimited|unlimited|
|Queue rules||24h trial|1|unlimited|unlimited|unlimited|unlimited|
|HotSpot active users||24h trial|1|1|200|500|unlimited|
|User manager active sessions||24h trial|1|10|20|50|Unlimited|
|Bonding interfaces||24h trial|1|unlimited|unlimited|unlimited|unlimited|
|RADIUS All Licenses:|never expire (a running and licensed router can be used indefinitely) can use unlimited number of interfaces are for one installation each offer unlimited software upgrades (exception-demo license does not allow ROS version upgrade (started from 7.8))|24h trial|-|unlimited|unlimited|unlimited|unlimited|

wifi-qcom drivers allows PTMP operations, regardless of license level. Mode: AP is universally available for all wifi-qcom devices, supporting multiple client stations.

### CHR License Levels

License levels described until now do not apply to Cloud Hosted Routers (CHRs). CHR is a RouterOS version intended for running as a virtual machine. It has its own 4 license levels as well as trial where you can test any of the paid license levels for 60 days.

60-day free trial license is available for all paid license levels. To get the free trial license, you have to have an account on MikroTik.com as all license management is done there.

Perpetual is a lifetime license (buy once, use forever). It is possible to transfer a perpetual license to another CHR instance. A running CHR instance will indicate the time when it has to access the account server to renew it's license. If the CHR instance will not be able to renew the license it will behave as if the trial period has ran out and will not allow an upgrade of RouterOS to a newer version.

After licensing a running trial system, you must manually run the /system license renew command from the CHR to make it active. Otherwise the system will not know you have licensed it in your account. If you do not do this before the system deadline time, the trial will end and you will have to do a complete fresh CHR installation, request a new trial and then license it with the license you had obtained.

License Speed Price Description limit

Free 1Mbit FREE The free license level allows CHR to run indefinitely. It is limited to 1Mbps upload per interface. All the rest of the features provided by CHR are available without restrictions. To use this, all you have to do is download disk image file from our download page and create a virtual guest. P1 1Gbit $45 P1 (perpetual-1) license level allows CHR to run indefinitely. It is limited to 1Gbps upload per interface. All the rest of the features provided by CHR are available without restrictions. It is possible to upgrade from P1 to P10 or P-Unlimited. Once the upgrade is purchased at the full price, the former license will become available for later use on your account. P10 10Gbit $95 P10 (perpetual-10) license level allows CHR to run indefinitely. It is limited to 10Gbps upload per interface. All the rest of the features provided by CHR are available without restrictions. It is possible to upgrade from P10 to P-Unlimited. Once the upgrade is purchased at the full price, the former license will become available for later use on your account. P-Unlimited $250 The p-unlimited (perpetual-unlimited) license level allows CHR to run indefinitely. It is the highest tier license and it has no Unlimited enforced limitations. 60-day FREE In addition to the limited Free installation, you can also test the increased speed of P1/P10/PU licenses with a 60 trial. Trial You will have to have an account registered on MikroTik.com. Then you can request the desired license level for trial from your router that will assign your router ID to your account and enable a purchase of the license from your account. All the paid license equivalents are available for trial. A trial period is 60 days from the day of acquisition, after this time passes, your license menu will start to show "Limited upgrades", which means that RouterOS can no longer be upgraded. Note that if you plan to purchase the selected license, you must do it before 60 days trial ends. If your trial has ended, and there are no purchases within 2 months, the device will no longer appear in your MikroTik account. You will have to make a new CHR installation to make a purchase within the required time frame. To request a trial license, you must run the command "/system license renew" from the CHR device command line. You will be asked for the username and password (sensitive) of your mikrotik.com account.

Warning: If you plan to use multiple virtual systems of the same kind, it may be possible that the next machine has the same SystemID as the original one. This can happen on certain cloud providers, such as Linode. To avoid this, after your first boot, run the command "/syste m license generate-new-id" before you request a trial license. Note that this feature must be used only while CHR is running on free type of RouterOS license. If you have already obtained paid or trial license, do not use regenerate feature since you will not be able to update your current key any more

To use multiple virtual machines, download the disk image from our webpage, and make as many copies, as you need virtual machines. Then make new virtual machine system from each virtual disk image.

Make sure to make copies of the Disk Image before you run or register the downloaded file.

### Prepaid Key

A Prepaid Key is a type of license key you can purchase in advance for MikroTik products, such as the CHR, or convert into a license key to apply to an x86 system's Software ID. It allows you to buy a license without immediately assigning it to a specific device. Once you have a Prepaid Key, you can use it to upgrade a CHR or later convert it into a license key by providing the device's Software ID.
