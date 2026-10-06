---
type: Reference
title: "Packages"
description: "RouterOS features are separated in \"packages\", which are files with .npk extension. Most of the features are combined in one routeros package, but some features are separate. Installing the corresponding NPK package can ."
timestamp: '2026-05-26'
status: active
tags: [routeros, mikrotik, networking]
resource: ~/Downloads/ROS-260526-1445-796.pdf
sources:
  - resource: https://manual.mikrotik.com/docs/introduction/
---

# Packages

Summary Minimum requirements Installing packages Manual download Download directly from the router Verification of install System packages Extra packages Working with packages Auto install Local Update Examples Listing packages

Summary

RouterOS features are separated in "packages", which are files with .npk extension. Most of the features are combined in one routeros package, but some features are separate. Installing the corresponding NPK package can enable specific features (like container, dude). Packages are provided only by MikroTik, and no 3rd parties are allowed to make them. You can download extra packages separately from our download page, or, since v7.18, it is possible to add extra packages directly from your router.

### Minimum requirements

RouterOS requires only the system package to operate at bare minimum, but for most devices normal operation and features are available when you install the "routeros" bundle package.

In case of wireless devices, several wireless packages are available, depending on the hardware you are using:

Starting from RouterOS 7.13, the routeros (system) package and one of the following wireless packages are needed for the basic operation of a simple home router.

1. 802.11ax WiFi APs require radio drivers, which are provided by the wifi-qcom package (for RouterOS version before 7.13 it was called the wifiwave2 package).
2. Previous generation WiFi APs require a wireless package.
More information about which wireless package to use is available in the Wireless manual.

Other packages are optional and not required for a home router. Install them only if you are sure of their purpose.

### Installing packages

Manual download

To manually download and install extra packages, download the necessary package from the MikroTik download page, selecting the RouterOS section based on your device's architecture found in the System/Resources menu. Extract the archive and upload the required package to your router using any convenient method, and proceed to reboot the router.

Download directly from the router

Since 7.18 it is possible to download/install extra packages directly from the router, using the System Packages section.

1. After executing the Check For Updates command, available packages will be listed in the Packages list, but they will show up as disabled. The available package list comes from the MikroTik download server. Those packages are available, but not yet in your router (as indicated by the flags X (Disabled) and A (available).
2. To download an extra package, first, select package and click Enable
3. To make the router download the package, click Apply Changes and the device will ask for a reboot
This feature is also shown in our v7.18 announcement video.

Package list After loading the list with "Check for updates" Enabling a package

Verification of install

To make sure package is installed successfully, check the "Log" section after the device is rebooted. If the package is installed successfully, you will see a message about it. If there have been conflicts or some requirement is not met, this will be explained, so you can take further steps to rectify that.

Success in the log entries

Failure in the log entries

|System packages|||
|---|---|---|
|Package|Description||
|routeros-arm (arm)|system package for arm devices||
|routeros-arm (arm64)|system package for arm64 devices||
|routeros-mipsbe (mipsbe)|system package for mipsbe devices||
|routeros-mmips (mmips)|system package for mmips devices||
|routeros-smips (smips)|system package for smips devices||
|routeros-tile (tile)|system package for tile devices||
|routeros-ppc (ppc)|system package for ppc devices||
|routeros (x86, CHR)|system package for x86 installations and CHR environment||
|Extra packages|||
|Package (supported architecture)||Description|
|calea (arm, arm64, mipsbe, mmips, tile,||Data gathering tool for specific use due to "Communications Assistance for Law Enforcement Act" in the|
|ppc, x86, CHR)||USA|
|container (arm, arm64, x86, CHR)||Container implementation of Linux containers, allows users to run containerized environments within RouterOS|
|dude (arm, arm64, mmips, tile, x86, CHR)||Dude tool that allows monitoring of network environment|

extra-nic (arm64)

gps (arm, arm64, mipsbe, mmips, tile, ppc, x86, CHR)

iot (arm, arm64, mipsbe, mmips, tile, ppc, x86, CHR)

iot-bt-extra (arm, arm64)

lora (arm, arm64, mipsbe, mmips, tile, ppc, x86, CHR)

lte (mipsbe)

rose-storage (arm, arm64, tile, x86, CHR)

switch-marvell (arm64)

tr069-client (arm, arm64, mipsbe, mmips, smips, tile, ppc, x86, CHR)

ups (arm, arm64, mipsbe, mmips, tile, ppc, x86, CHR)

user-manager (arm, arm64, mipsbe, mmips, tile, ppc, x86, CHR)

wifi-qcom (arm, arm64)

wifi-qcom-ac (arm)

wireless (arm, arm64, mipsbe, mmips, tile, ppc, x86, CHR)

zerotier (arm, arm64)

### Working with packages

Menu: /system package

Command Description

disable

enable

uninstall

arm64 CPU architecture, Network Interface Card(NIC) support, recommended for UEFI installation on non MikroTik boards

Global Positioning System devices support

Enables:

MQTT LoRa (for devices with LR8/9/2 miniPCie cards) Bluetooth (for devices with Bluetooth chip) GPIO (for devices with GPIO pins) Modbus (for devices with RS485 port)

A package for ARM, ARM64 devices which enables the use of USB Bluetooth adapters (must support LE

4.0+). note: Not all adapters were tested. We can not guarantee beforehand that a specific adapter will work. Dummy package for Lora support. LoRa package is not obligatory anymore and is left only for compatibility reasons. LoRa functionality is moved into iot package. Required package only for SXT LTE (RBSXTLTE3-7), which contains drivers for the built-in LTE interface. Additional enterprise data center functionality in RouterOS, support disk monitoring, improved formatting, RAIDs, rsync, iSCSI, NVMe over TCP, NFS, and improved SMB Mandatory driver package for CRS8xx series switches. TR069 Client package APC ups management interface MikroTik User Manager server for controlling Hotspot and other service users. Mandatory driver package for 802.11ax interfaces. Introduced in 7.13.  Wifi CAPsMAN support comes with the system package. Optional Wifi driver package for compatible 802.11ac interfaces. Introduced in 7.13. Utilities and drivers for managing WiFi (up to 802.11ac) and 60GHz wireless interfaces. This package is bundled into RouterOS for versions up to 7.12. Starting with 7.13, it is a separate package. The wireless package conflicts with wifi-qcom and wifi-qcom-ac packages-they cannot be active at the same time. Enables ZeroTier functionality
Commands executed in this menu will take place only on restart of the router. Until then, the user can freely schedule or revert set actions.

schedule the package to be disabled after the next reboot. No features provided by the package will be accessible

downgrade will prompt for the reboot. During the reboot process will try to downgrade the RouterOS to the oldest version possible by checking the packages that are uploaded to the router.

schedule package to be enabled after the next reboot

schedule package to be removed from the router. That will take place during the reboot.

unschedule remove scheduled task for the package.

print outputs information about the packages, like: version, package state, planned state changes, etc.

update manages the "check-for-updates" channel and performs RouterOS upgrades

apply-apply scheduled changes and reboot device changes

Menu: /system/check-installation

The "Check installation" function ensures the integrity of the RouterOS system by verifying the readability and correct placement of files. Its primary purpose is to confirm the health and status of your NAND/Flash storage.

Menu: /system/package/update install ignore-missing command allows upgrading only the RouterOS main package, while omitting packages that are either missing or not uploaded during a manual upgrade process.

### Auto install

It is also possible to automatically install packages after uploading them to the router with FTP or SFTP. The package file must be named with the extension *.auto.npk. Once the file will be uploaded, router will automatically go into reboot in order to install the package.

".auto.npk" in the filename is mandatory for a package to be automatically installed.

### Local Update

Instead of connecting directly to MikroTik servers you can upload package files to one of your local RouterOS device, and use it as a local package server.

Menu: /system package local-update

Command Description

download-all Downloads all compatible (matching device architecture) packages that are available on the local package server. Downloaded packages are saved in root directory.

download Downloads specific compatible (matching device architecture) packages that are available on the local package server. Downloaded packages are saved in root directory.

refresh Refreshes/checks the list of available compatible (matching device architecture) packages on the local package server.

Server from which to get the package can be defined in system/package/local-update/ update-package-source/

update-package-source properties list:

Property Description

address (IPv4 address [IPv4]/IPv6 address [IPv6]; Default: ) Address of the local package server.

user (string; Default: ) Username that is used for accessing the local package server.

password (string; Default: ) sensitive Password that is used for accessing the local package server.

Also, you can mirror packages (for all architectures) from your main local package server using system/package/local-update/mirror/ Downloaded packages saved into packs folder in root directory. mirror properties list:

Property Description

primary-server (IPv4 address Address of the primary local package server. [IPv4]/IPv6 address [IPv6]; Defaul t: )

secondary-server (IPv4 address Address of the secondary local package server. [IPv4]/IPv6 address [IPv6]; Defaul t: )

|ve|user (string; Default:) password (string; Default:) sensiti check-interval (time [HH:MM:SS]; Default: 24:00:00) enabled (yes | no; default: no) Menu: /system package local-update mirror|Username that is used for accessing the local package server. Password that is used for accessing the local package server. Time interval at which device checks the local package server for new packages availability, if new package /packages is located begins package download. (only downloads the packages that are not already present on the device) Whether to enable or no the periodical check and download of packages from the local package server.|
|---|---|---|
|Command|Description||
|force-check Examples|Listing packages scheduled for uninstall. /system package print Flags: X-DISABLED Columns: NAME, VERSION, SCHEDULED 2 routeros 7.9 3 XA iot 7.9|Checks the local package server for new packages availability, if new package/packages is located begins package download. (only downloads the packages that are not already present on the device) zerotier package is disabled, but installed; iot package is available on the server, but has not been downloaded to the router and enabled; dude package is # NAME VERSION SCHEDULED 0 dude 7.9 scheduled for uninstall 1 X zerotier 7.9|
|Uninstall package|Reboot, yes? [y/N]:|/system package uninstall dude; /system reboot;|
|Disable package|Reboot, yes? [y/N]:|/system package disable zerotier; /system reboot;|
|Downgrade|Reboot, yes? [y/N]: Cancel uninstall or disable action /system package unschedule zerotier; /system package unschedule dude;|/system package downgrade; /system reboot;|
